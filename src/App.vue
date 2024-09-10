<script>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Btn from '@/components/Btn.vue';

export default {
  components: {
    Btn,
  },

  data() {
    return {
      isShow: true,
    }
  },

  created() {
    this.isShow = true;
  },

  methods: {
    setShow() {
      this.isShow = false;
      this.$router.push('/order');
    }
  }
}

</script>

<template>
  <div>
    <nav class="nav">
      <!-- <RouterLink to="/">Home</RouterLink> -->
      <Btn @click="setShow">
        前往報名
      </Btn>
      <h1 class="title">自然環境觀賞報名系統</h1>
    </nav>
    
  </div>
  
  <div class="picture">
    <RouterView />
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.picture {
  background-image: url(@/assets/img/images.jpg);
  width: 100%;
  height: 100vh;
  background-size: cover;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
  background: linear-gradient(to right, rgb(9, 68, 54), rgb(128, 197, 231));
  padding: 10px;
  display: flex;
  align-items: center;
}

.nav{
  padding-left: 50px;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

.title{
  color: white;
  font-size: 32px;
  margin-left: 10%;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }

  body {
    background: linear-gradient(to right, rgb(227, 212, 182), rgb(111, 194, 235));
  }
}
</style>
