<template>
  <div>
    <button @click="toggleView()">toggle</button>
    <div v-if="this.slotView">
      <slot-pick :userdata="userdata"></slot-pick>
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
      };
    },
  };
</script>

<style>
</style>
