<script>
import Btn from '@/components/Btn.vue';
import Card from '@/components/Card.vue';
import { onUnmounted } from 'vue';
import Swal from 'sweetalert2'

export default {
  components: {
    Btn,
    Card,
    
  },

  data() {
    return {
      data: [
        { name: '', img: '', id: new Date().getTime(), email: '', phone: '', gender: '', meal: '', time: '', idNumber: '', contractTime: [] }
      ],
      isSubmit: false,
    }
  },

  methods: {
    addCard() {
      this.data.push({ name: '', img: '', id: new Date().getTime(), email: '', phone: '', gender: '', meal: '', time: '', idNumber: '', contractTime: [] });
    },
    setClick() {
      
      this.setStorage();
      Swal.fire({
        title: "報名成功",
        icon: "success"
      }).then((result) => {
        if (result.isConfirmed) {
          //js內跳vue-router的頁面
          this.$router.push('/result');
        }
      });
    },

    deleteItem(id) {
      const index = this.data.findIndex(item => item.id === id);
      this.data.splice(index, 1);
    },

    setStorage() {
      sessionStorage.setItem('object', JSON.stringify(this.data));
    },

    goHome() {
      this.$router.push('/');
    },

    goResult() {
      this.$router.push('/result');
    }
  }
}
</script>
<template>
  <div class="nav">
    <h1 class="title">報名頁面</h1>
    <Btn @click="goHome">
      回到首頁
    </Btn>
    <Btn @click="addCard">
      新增報名
    </Btn>

    <Btn class="goResult" @click="setClick">
      送出報名
    </Btn>

  </div>

  <div class="container">
    <Card v-for="(item, index) in data" :key="index" :orderObj="this.data[index]" @delete="deleteItem"></Card>
  </div>
</template>

<style scoped>
.nav {
  display: flex;
  padding: 10px;
  background: linear-gradient(to right, rgb(34, 33, 120), rgb(129, 230, 238));
  align-items: center;
}

.title {
  color: white;
}

.container {
  display: flex;
  flex-wrap: wrap;
}

body {
  background: linear-gradient(to right, rgb(227, 212, 182), rgb(111, 194, 235));
}
</style>
