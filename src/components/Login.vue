<template>
  <div class="wrapper">
    <label>Username</label>
    <input type="text"/>
    <label>Password</label>
    <input type="text"/>
    <button>
      Login
    </button>
    <div>
      <a href="#">Signup</a>
      <a href="#">forgot password</a>
    </div>
  </div>
</template>

<script>
</script>

<style>
  .wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center
  }
  div {
    margin: 10px 0;
  }
  input {
    height: 1.5rem;
  }
  button {
    margin: 10px 0;
  }
  a {
    margin: 0 10px;
  }
</style>
