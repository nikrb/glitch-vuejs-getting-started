<template>
<div v-if="!isEditing" class="todo-wrapper">
  <div class="item-buttons">
    <button class="edit-button" type="button" @click="toggleTodoEditForm"></button>
    <button class="delete-button" type="button" @click="deleteTodo"></button>
    <input class="todo-checkbox" type="checkbox" :id="id" :checked="isDone"
           @change="$emit('checkbox-changed')"/>
    <label :for="id">{{label}}</label>
  </div>
</div>
<todo-item-edit-form v-else :id="id" :label="label"
                     @item-edited = "itemEdited"
                     @edit-cancelled = "editCancelled"
                     ></todo-item-edit-form>
</template>

<script>
  import TodoItemEditForm from './TodoItemEditForm.vue';
  export default {
    name: 'TodoItem',
    components: {
      TodoItemEditForm,
    },
    props: {
      id: { required: true, type: String},
      label: { required: true, type: String},
      done: { default: false, type: Boolean},
    },
    methods: {
      deleteTodo(){
        this.$emit('item-deleted');
      },
      toggleTodoEditForm(){
        this.isEditing = true;
      },
      itemEdited(newLabel) {
        this.$emit('item-edited', newLabel);
        this.isEditing = false;
      },
      editCancelled() {
        this.isEditing = false;
      }
    },
    computed: {
      isDone() {
        return this.done;
      }
    },
    data() {
      return {
        isEditing: false,
      }
    }
  };
</script>

<style>
  li {
    list-style-type: none;
  }
  button {
    margin: 2px;
  }
  .edit-button {
    width: 20px;
    height: 20px;
    background-image: url("https://img.icons8.com/ios-glyphs/30/000000/edit--v1.png");
    background-size: contain;
  }
  .delete-button {
    width: 20px;
    height: 20px;
    background-image: url("https://img.icons8.com/ios-glyphs/30/000000/filled-trash.png");
    background-size: contain;
  }
  .item-buttons {
    width: 100%;
    display: flex;
    align-items: center;
    padding: 2px;
  }
  .item-buttons label {
    display: flex;
    align-items: center;
    padding-right: 5px;
  }
  .todo-checkbox {
    width: 20px;
    height: 20px;
  }
  .todo-wrapper {
    width: 100%;
    display: flex;
    justfiy-content: center;
  }
</style>