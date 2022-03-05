<template>
  <div>
    <slots :userdata="userdata"></slots>
  </div>
</template>

<script>
  import Slots from './Slots.vue'
  export default {
    name: "AdminPage",
    props: {
      userdata: {required: true, type:Array},
    },
    components: {
      Slots,
    },
  };
</script>

<style>
</style>
