<template>
  <div id="app">
    <h1>Todo Component</h1><button @click="test()">
    test
  </button>
    <todo :todolist="todolist"></todo>
  </div>
</template>

<script>
  import Todo from './components/Todo.vue';
  import uniqueId from 'lodash.uniqueid';

export default {
  name: 'app',
  components: {
    Todo,
  },
  methods: {
    test() {
      for( let item in this.todolist)
        console.log( this.todolist[item].label);
    }
  },
  data() {
    return {
      todolist: [
          { id: uniqueId('todo-'), label: "item 1", done: false},
          { id: uniqueId('todo-'), label: "item 2", done: true},
        ]
    }
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
