<template>
  <div>
    <p>
      2
    </p>
    <div>
      <label>course</label>
      <select v-model="coursekey">
        <option v-for="c in courseList" :key="c.id" :value="c.id">{{c.name + "(level"+c.level+")"}}</option>
      </select>
    </div>
    <button @click="toggleView()">toggle</button>
    <div v-if="this.slotView">
      <slot-pick :userdata="userdata" :course-list="courseList" :coursekey="coursekey"></slot-pick>
    </div>
    <div v-else>
      <slots :userdata="userdata"></slots>
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
    },
    data() {
      return {
        slotView: true,
        coursekey: '',
      };
    },
  };
</script>

<style>
</style>
