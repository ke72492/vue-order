<script>
import Btn from '@/components/Btn.vue';
import Card from '@/components/Card.vue';

export default {
    components: {
        Btn,
        Card,
    },

    data() {
        return {
            data: [],
        }
    },

    mounted() {
        setTimeout(() => {
            const jsonData = this.getStorage();
            this.data = jsonData;
        }, 1000)


    },

    methods: {
        getMessage(data) {
            this.data.push(data);
            // console.log(this.data);
        },
        getStorage() {
            const jsonStorage = sessionStorage.getItem('object');
            if (!JSON.parse(jsonStorage)) {
                return [];
            }
            return JSON.parse(jsonStorage);
        },
        goHome() {
            this.$router.push('/');
        }
    }
}
</script>
<template>
    <nav>
        <h1 class="title">報名結果頁</h1>
        <Btn @click="goHome">
            回到首頁
        </Btn>

    </nav>
    <div class="container">

        <Card v-for="item in data" :key="item.id" :orderObj="item" disabled />
    </div>
</template>

<style scoped>
table {
    margin: 10px;
}

table,
th,
td {
    border: 1px solid black;
    text-align: center;
    font-size: 18px;
}

th,
td {
    width: 100px;
    min-height: 50px;
}

.card {
    background: linear-gradient(to right, rgb(53, 233, 191), rgb(128, 197, 231));
}

body {
    background: linear-gradient(to right, rgb(227, 212, 182), rgb(111, 194, 235));
}

nav {
    display: flex;
    padding: 10px;
    background: linear-gradient(to right, rgb(34, 33, 120), rgb(129, 230, 238));
    align-items: center;
}

.title {
  color: white;
}

.container{
    display: flex;
    flex-wrap: wrap;
}
</style>
