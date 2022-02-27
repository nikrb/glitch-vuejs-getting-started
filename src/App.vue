<template>
  <div id="app">
    <h1>Availability</h1>
    <button @click="test()">Test</button>
    <availability-table :cells="this.Cells"></availability-table>
  </div>
</template>

<script>
  import AvailabilityTable from './components/AvailabilityTable.vue';
  import uniqueId from 'lodash.uniqueid';

export default {
  name: 'app',
  components: {
    AvailabilityTable,
  },
  methods: {
    test() {
      console.log("test:", this.Cells);
    }
  },
  data() {
    let newcells = new Array(24);
    for( let i =0; i<24; i++) {
      newcells[i] = new Array(7);
      for( let j=0; j<7; j++) {
        newcells[i][j] = {id: uniqueId("slot"), available:Math.random()>0.5?true:false};
      }
    }
    return {
      Cells: newcells,
    };
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
