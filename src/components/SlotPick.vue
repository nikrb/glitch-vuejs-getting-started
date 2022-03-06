<template>
  <div>
    <div>
      <label>day</label>

      <select @change="updateList()" v-model="daykey">
        <option value="0">Monday</option>
        <option value="1">Tuesday</option>
        <option value="2">Wednesday</option>
        <option value="3">Thursday</option>
        <option value="4">Friday</option>
        <option value="5">Saturday</option>
        <option value="6">Sunday</option>
      </select>
    </div>
    <div>
      <label>hour</label>
      <select @change="updateList()" v-model="hourkey">
        <option v-for="i in 24" :key="i">{{i-1}}</option>
      </select>
    </div>
    <div style="display: flex; flex-direction: column">
      <label v-for="i in available" :key="i">{{i}}</label>
    </div>
  </div>
</template>

<script>
  export default {
    name: "SlotPick",
    props: {
      userdata: { required: true, type: Array},
    },
    methods: {
      dayChange() {
        console.log("day change:", this.daykey);
      },
      hourChange() {
        console.log("hour change:", this.hourkey);
      },
      updateList() {
        const list = [];
        const daykey = this.daykey;
        const hourkey = this.hourkey;
        this.userdata.forEach(function(e) {
          console.log("user:", e);
          console.log("day,hour:", daykey, hourkey);
          if(e.slots[hourkey][daykey].available){
            list.push(e.name);
          }
        });
        this.available = list;
        console.log("new list:", list);
      },
    },
    data() {
      return {
        daykey: 0,
        hourkey: 0,
        available: [],
      };
    },
    
  };
</script>

<style>
</style>
