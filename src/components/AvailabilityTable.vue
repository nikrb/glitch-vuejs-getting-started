<template>
<div>
  <div>
    <button @click="courseViz()">Courses</button>
    <div :class="{ 'courses-hidden': !coursesVisible}">
      <div v-for="c, i in userCourseMap" :key="c.id">
        <input type="checkbox"
              v-model="userCourseMap[i].hasCourse"
              :value="c.hasCourse"
              @change="$emit('user-course-changed', userCourseMap[i])"/>
        <label>{{c.name + "(level "+c.level+")"}}</label>
      </div>
    </div>
  </div>
  <button @click="clear()">clear</button>
  <table @mouseleave="mouseOutOfBounds()">
    <tr @mouseenter="mouseOutOfBounds()">
      <th></th>
      <th v-for="day in dow" :key="day">{{day.charAt(0)}}</th>
    </tr>
    <tr v-for="(row ,i) in cells" :key="i">
      <td @mouseenter="mouseOutOfBounds()">{{i}}</td>
      <td v-for="cell in row" :key="cell.id"
          :class="{ 'available': cell.available}"
          @mousedown="mouseDown(cell)"
          @mouseover="mouseOver(cell)"
          @mouseup="mouseUp()">
      </td>
    </tr>
  </table>
</div>
</template>

<script>
  export default {
    name: "AvailabilityTable",
    props: {
      userdata: Object,
      courseList: Array,
    },
    methods: {
      clear() {
        this.cells = this.cells.map(hour => hour.map(day => { return { ...day, available : false};}));
      },
      mouseDown(cell) {
        this.isMouseDown = true;
        cell.available = !cell.available;
        this.$emit('available-changed', cell);
      },
      mouseOver(cell) {
        if( this.isMouseDown){
          cell.available = !cell.available;
          this.$emit('available-changed', cell);
        }
      },
      mouseUp() {
        this.isMouseDown = false;
      },
      mouseOutOfBounds() {
        this.isMouseDown = false;
      },
      courseViz() {
        this.coursesVisible = !this.coursesVisible;
      },
      hasCourse(course) {
        const has = this.userdata.courses.filter(c => c.id == course.id);
        return has.length > 0;
      }
    },
    data() {
      console.log("running AvailabilityTable data function:", this.userdata);
      return {
        isMouseDown: false,
        dow: ["M","T","W","Th","F","Sa","Su"],
        cells: this.userdata.slots,
        userCourseMap: this.courseList.map(c => {
          return {
            hasCourse: this.hasCourse(c),
            ...c
          };
        }),
        coursesVisible: true,
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
  .courses-hidden {
    display: none;
  }
</style>
