<template>
  <div id="app">
    <h1>Availability</h1>
    <availability-table></availability-table>
  </div>
</template>

<script>
  import AvailabilityTable from './components/AvailabilityTable.vue';

export default {
  name: 'app',
  components: {
    AvailabilityTable,
  },
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
