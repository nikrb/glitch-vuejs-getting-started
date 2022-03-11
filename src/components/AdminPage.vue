<template>
  <div>
    <div>
      <label>course</label>
      <select v-model="coursekey">
        <option v-for="c in courseList" :key="c.id" :value="c.id">{{c.name + "(level"+c.level+")"}}</option>
      </select>
    </div>
    <button @click="toggleView()">toggle</button>
    <div v-if="this.slotView">
      <slot-pick :userdata="availableuserdata"></slot-pick>
    </div>
    <div v-else>
      <slots :userdata="availableuserdata"></slots>
    </div>
  </div>
</template>

<script>
  import Slots from './Slots.vue';
  import SlotPick from './SlotPick.vue';
  export default {
    name: "AdminPage",
    props: {
      userdata: {required: true, type:Array},
      courseList: {required: true, type: Array},
    },
    components: {
      Slots,
      SlotPick,
    },
    methods: {
      toggleView(){
        this.slotView = !this.slotView;
      },
      availableForCourse(alldata){
        const coursekey = this.coursekey;
        const ret = alldata.filter(u => u.courses.filter(c => c.id == coursekey).length);
        return ret;
      },
    },
    watch: {
      coursekey: function() {
        this.availableuserdata = this.availableForCourse(this.userdata);
      },
    },
    data() {
      return {
        slotView: true,
        coursekey: '',
        availableuserdata: this.availableForCourse(this.userdata),
      };
    },
  };
</script>

<style>
</style>
