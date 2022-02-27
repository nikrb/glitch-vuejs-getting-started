<template>
  <form @submit.prevent="onSubmit">
    <label for="new-todo-input">Todo </label>
    <input
           type="text"
           id="new-todo-input"
           name="new-todo"
           autocomplete="off"
           v-model.lazy.trim="label" />
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  methods: {
    onSubmit() {
      if( this.label === "") return;
      console.log('new todo form submitted:', this.label);
      this.$emit("todo-added", this.label);
      this.label = "";
    }
  },
  data() {
    return {
      label: "",
    };
  }
};
</script>

