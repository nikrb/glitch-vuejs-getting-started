<template>
<div>
  <p>7</p>
  <textarea rows="4" cols="20" v-model="availability" placeholder="Availability"></textarea>
  <table>
    <tr>
      <th></th>
      <th v-for="day in dow" :key="day">{{day.charAt(0)}}</th>
    </tr>
    <tr v-for="row in 24" :key="row">
      <td>{{row}}</td>
      <td v-for="col in 7" :key="(row-1)*24+col"
          @mouseover="mouseOver({row,col})">
      </td>
    </tr>
  </table>
</div>
</template>

<script>
  export default {
    name: "Slots",
    props: {
      userdata: Array, // [{name, slots},...]
    },
    methods: {
      mouseOver(cell) {
        const row = cell.row-1;
        const col = cell.col-1;
        
        this.availability = [];
        for( let i = 0; i<this.userdata.length; i++){
          let user = this.userdata[i];
          let name = user.name;
          let week = user.slots[row];
          let avail = week[col];
          if(avail.available) this.availability.push(name);
        }
        // console.log("day,hour,available:", this.dow[col], row, this.availability);
      },
    },
    data() {
      console.log("running data function:", this.userdata);
      return {
        isMouseDown: false,
        dow: ["M","T","W","Th","F","Sa","Su"],
        availability: []
      };
    }
  };
</script>

<style>
  table {
    border: 1px solid;
    border-collapse: collapse;
  }
  td:nth-child(1):hover {
    border: 1px solid;
    border-collapse: collapse;
  }
  td, th {
    width: 20px;
    height: 20px;
    border: 1px solid;
    border-collapse: collapse;
    user-select: none;
  }
  td:hover {
    border-color: yellow;
  }
  .available {
    background-color: lightgreen;
  }
</style>
