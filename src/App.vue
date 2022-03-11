<template>
  <div id="app">
    <h1>Availability6</h1>
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
      user: {name:"joe", isAdmin: false},
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
  button {
    display: inline-block;
    margin-bottom: 0;
    font-weight: 400;
    font-size: 1rem;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    -ms-touch-action: manipulation;
    touch-action: manipulation;
    cursor: pointer;
    color: white;
    background-color: #00A2FF;
    border: 1px solid transparent;
    padding: 6px 12px;
    line-height: 1.42857143;
    border-radius: 4px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
  button:focus {
    border: 1px solid black;
  }
  button:hover {
    background-color: #0082dF;
  }
  table {
    margin-top: 10px;
  }
</style>
