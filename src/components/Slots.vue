<template>
<div>
  <div :style="{left: 'calc(50vw - 90px)', top: this.top, position: 'fixed'}">
    <textarea rows="4" cols="20" v-model="availability" placeholder="Availability" resize="none"></textarea>
  </div>
  <table @mouseleave="mouseLeave()">
    <tr>
      <th></th>
      <th v-for="day in dow" :key="day">{{day.charAt(0)}}</th>
    </tr>
    <tr v-for="row in 24" :key="row">
      <td>{{row}}</td>
      <td v-for="col in 7" :key="(row-1)*24+col"
          @mouseover="mouseOver({row,col},$event)">
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
      mouseOver(cell, event) {
        const row = cell.row-1;
        const col = cell.col-1;
        if(row != this.last_row) {
          const dir = row > this.last_row;
          if(dir) {
            this.top = event.clientY - 100 +"px";
          } else {
            this.top = event.clientY +"px";
          }
          this.last_row = row;
        }
        
        this.availability = [];
        for( let i = 0; i<this.userdata.length; i++){
          let user = this.userdata[i];
          let name = user.name;
          let week = user.slots[row];
          let avail = week[col];
          if(avail.available) this.availability.push(name);
        }
      },
      mouseLeave() {
        this.top = "0px";
        this.last_row = -1;
      },
    },
    data() {
      console.log("running data function:", this.userdata);
      return {
        isMouseDown: false,
        dow: ["M","T","W","Th","F","Sa","Su"],
        availability: [],
        left: 0,
        top: 0,
        last_row: -1,
      };
    }
  };
</script>

<style>
  textarea {
    border: 1 solid blue;
  }
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
