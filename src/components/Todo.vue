<template>
  <div class="todo-form-wrapper">
    <p id="list-summery">{{listSummary}}</p>
    <todo-form @todo-added="addTodo"></todo-form>
    <ul>
      <li v-for="item in TodoList" :key="item.id">
        <todo-item :label="item.label" :done="item.done" :id="item.id"
                   @checkbox-changed="updateDoneStatus(item.id)"
                   @item-deleted="deleteTodo(item.id)"
                   @item-edited="editTodo(item.id, $event)"
                   ></todo-item>
      </li>
    </ul>
  </div>
</template>

<script>
  import TodoItem from './TodoItem.vue';
  import TodoForm from './TodoForm.vue';
  import uniqueId from 'lodash.uniqueid';
  
  export default {
  name: "Todo",
  components: {
    TodoItem,
    TodoForm,
  },
  props: {
    todolist: { required: true, type: Array}
  },
  methods: {
    addTodo(todo_label) {
      console.log( "todo added:", todo_label);
      this.TodoList.push({ id: uniqueId('todo-'), label: todo_label, done: false});
    },
    updateDoneStatus(todo_id) {
      const update_todo = this.TodoList.find(i => i.id === todo_id);
      update_todo.done = !update_todo.done;
    },
    deleteTodo(todo_id) {
      const ndx = this.TodoList.findIndex(item => item.id === todo_id);
      this.TodoList.splice(ndx,1);
    },
    editTodo(todo_id, new_label) {
      const todo2edit = this.TodoList.find(item => item.id === todo_id);
      todo2edit.label = new_label;
    }
  },
  computed: {
    listSummary() {
      const finishedItems = this.TodoList.filter(i=>i.done).length;
      return `${finishedItems} out of ${this.TodoList.length} items completed`;
    }
  },
  data() {
    return {
      TodoList: this.todolist,
    }
  }
  };
</script>

<style>
  ul {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    padding: 0;
  }
  li {
    display: flex;
    justify-content: flex-start;
  }
  .todo-form-wrapper {
    display: flex;
    flex-direction: column;
  }
</style>
