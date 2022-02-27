<template>
<div>
  <p>14</p>
  <button @click="test()">test</button>
  <table>
    <tr>
      <th></th>
      <th v-for="day in dow" :key="day">{{day.charAt(0)}}</th>
    </tr>
    <tr v-for="(row ,i) in cells" :key="i">
      <td>{{i}}</td>
      <td v-for="cell in row" :key="cell.id"
          :id="cell.id"
          :class="{ 'available': cell.available}"
          @click="cellClicked(cell)">
      </td>
    </tr>
  </table>

</div>
</template>

<script>
  export default {
    name: "AvailabilityTable",
    props: {
      cells: {required: true, type:Array},
    },
    methods: {
      cellClicked(cell) {
        cell.available = !cell.available;
        console.log("cell clicked:", cell);
      },
      test() {
        /*
        let newcells = new Array(24);
        for( let i =0; i<24; i++) {
          newcells[i] = new Array(7);
          for( let j=0; j<7; j++) {
            newcells[i][j] = {id: i*7+j, available:Math.random()>0.5?true:false};
          }
        }
        console.log("cells:", newcells);
        this.cells = newcells;
        */
        console.log(this.cells);
      },
    },
    data() {
      return {
        dow: ["M","T","W","Th","F","Sa","Su"],
      };
    }
  };
</script>

<style>
  table {
    border: 1px solid;
    border-collapse: collapse;
  }
  td {
    width: 20px;
    height: 20px;
    border: 1px solid;
    border-collapse: collapse;
  }
  td:hover {
    border-color: yellow;
  }
  .available {
    background-color: lightgreen;
  }
</style>
