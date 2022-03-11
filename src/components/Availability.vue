<template>
  <div>
    <button @click="toggleAdmin">{{this.isAdmin?'admin':'user'}}</button>
    <admin-page v-if="isAdmin" :userdata="allUserData" :course-list="courseList"></admin-page>
    <div v-else>
      <h1>{{user.name}}</h1>
      <availability-table :userdata="loggedInUserData"
                          :course-list="courseList"
                          @user-course-changed="userCourseChanged"
                          @available-changed="userAvailableChanged">
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
        for( let hour in this.loggedInUserData.slots) {
          for( let day in hour) {
            if(day.id == cell.id) {
              day.available = cell.available;
            }
          }
        }
      },
      toggleAdmin() {
        this.isAdmin = !this.isAdmin;
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
        const usersdata = [{
            name: "Joe",
            courses: [course_list[4], course_list[5]],
            slots: this.makeSlots(),
          },{
            name: "Jon",
            courses: [course_list[0], course_list[6]],
            slots: this.makeSlots(),
        }];
      return {
        isAdmin: this.user.isAdmin,
        courseList: course_list,
        loggedInUserData: usersdata[0],
        allUserData: usersdata,
      }
    },
  };
</script>

<style>
</style>
