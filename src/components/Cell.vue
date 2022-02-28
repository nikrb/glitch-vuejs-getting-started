<template>
  <td :class="{ 'available' : available }"></td>
</template>

<script>
export default {
  name: "Cell",
  props: {
    id: {required: true, type:Number},
    available: {required: true, type:Boolean},
  }
};
</script>

<style>
  td {
    width:20px;
    height: 20px;
    border: 1px solid;
    border-collapse: collapse;
  }
  .available {
    background-color: green;
  }
  td:hover {
    background-color: yellow;
  }
</style>