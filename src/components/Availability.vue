<template>
  <div>
    <admin-page v-if="isAdmin" :userdata="getAllUserData()"></admin-page>
    <div v-else>
      <h1>{{user.name}}</h1>
      <availability-table :userdata="getLoggedInUserData()"
                          :courseList="courseList"
                          @userCourseChanged="userCourseChanged"
                          @availableChanged="userAvailableChanged">
      </availability-table>
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
      user: {required: true, type:Object}, // {name, isAdmin}
    },
    components: {
      AdminPage,
      AvailabilityTable,
    },
    methods: {
      getLoggedInUserData() {
        return this.loggedInUserData;
      },
      getAllUserData() {
        let data = [{
          name: "Joe",
          courses: [this.courseList[4], this.courseList[5]],
          slots: this.makeSlots(),
        },{
          name: "Jon",
          courses: [this.courseList[0], this.courseList[6]],
          slots: this.makeSlots(),
        }];
        return data;
      },
      userCourseChanged(course) {
        const found = this.loggedInUserData
              .courses.filter(c => c.id != course.id);
        if(found.length < this.loggedInUserData.courses.length) {
          this.loggedInUserData.courses = found;
        } else {
          let {hasCourse, // eslint-disable-line no-unused-vars
                ...rest} = course;
          this.loggedInUserData.courses.push(rest);
        }
      },
      userAvailableChanged(cell) {
        for( let week in this.loggedInUserData.slots) {
          for( let day in week) {
            if(day.id == cell.id) {
              day.available = cell.available;
            }
          }
        }
      },
      makeSlots() {
        // generate some availability
        let newcells = new Array(24);
        for( let i =0; i<24; i++) {
          newcells[i] = new Array(7);
          for( let j=0; j<7; j++) {
            newcells[i][j] = {
              id: uniqueId("slot"),
              available:(i<14 || i>16)? false : Math.random()>0.5?true:false,
            };
          }
        }
        return newcells;
      },
    },
    data() {
      const course_list = [
          {id: uniqueId('course'), level: 1, track: "gaming", name: "Scratch"},
          {id: uniqueId('course'), level: 1, track: "art", name: "Digital Creativity"},
          {id: uniqueId('course'), level: 1, track: "programming", name: "Python"},
          {id: uniqueId('course'), level: 2, track: "programming", name: "Python"},
          {id: uniqueId('course'), level: 1, track: "programming", name: "web"},
          {id: uniqueId('course'), level: 2, track: "programming", name: "javascript"},
          {id: uniqueId('course'), level: 2, track: "art", name: "3D Modelling"},
        ];
      return {
        isAdmin: this.user.isAdmin,
        courseList: course_list,
        loggedInUserData: {
          name: "Joe",
          courses: [course_list[4], course_list[5]],
          slots: this.makeSlots(),
        },
      }
    },
  };
</script>

<style>
</style>
