<template>
  <div>
    <admin-page v-if="isAdmin" :userdata="getAllUserData()"></admin-page>
    <div v-else>
      <h1>{{user.name}}</h1>
      <availability-table :userdata="getLoggedInUserData()"></availability-table>
    </div>
  </div>
</template>

<script>
  import AdminPage from "./AdminPage.vue";
  import AvailabilityTable from "./AvailabilityTable.vue";
  import uniqueId from 'lodash.uniqueid';
  
  export default {
    name: "Availability",
    props: {
      user: {required: true, type:Object}
    },
    components: {
      AdminPage,
      AvailabilityTable,
    },
    methods: {
      getLoggedInUserData() {
        return this.makeSlots();
      },
      getAllUserData() {
        let data = [{
          name: "Joe",
          courses: ["web","scratch", ]
          slots: this.makeSlots(),
        },{
          name: "Jon",
          slots: this.makeSlots(),
        }];
        return data;
      },
      makeSlots() {
        // generate some availability
        let newcells = new Array(24);
        for( let i =0; i<24; i++) {
          newcells[i] = new Array(7);
          for( let j=0; j<7; j++) {
            newcells[i][j] = {
              id: uniqueId("slot"),
              available:Math.random()>0.5?true:false,
            };
          }
        }
        return newcells;
      },
    },
    data() {
      return {
        isAdmin: this.user.isAdmin,
        courseList: [{
          {id: uniqueId('course'), level: 1, track: "gaming", name: "Scratch"},
          {id: uniqueId('course'), level: 1, track: "art", name: "Digital Creativity"},
          {id: uniqueId('course'), level: 1, track: "programming", name: "Python"},
          {id: uniqueId('course'), level: 2, track: "programming", name: "Python"},
          {id: uniqueId('course'), level: 2, track: "art", name: "3D Modelling"},
        }],
      }
    },
  };
</script>

<style>
</style>
