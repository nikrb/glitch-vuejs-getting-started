<template>
  <div id="app">
    <h1>Availability</h1>
    <div v-if="isLoggedIn">
      <availability :user="user"></availability>
    </div>
    <div v-else>
      <login></login>
    </div>
  </div>
</template>

<script>
  import Login from './components/Login.vue';
  import Availability from './components/Availability.vue';

export default {
  name: 'app',
  components: {
    Availability,
    Login,
  },
  data() {
    return {
      user: {name:"jon", isAdmin: false},
      isLoggedIn: true,
    }
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
