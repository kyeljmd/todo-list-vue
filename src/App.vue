<template>
  <div id="app">
    <h1 class="col-sm-12">TODO App</h1>
    <div class='col-sm-12'>
      <div class='container'>
        <todo-list v-bind:todos="todos"></todo-list>
        <create-todo v-on:create-todo="createTodo"></create-todo>
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from './components/TodoList';
import CreateTodo from './components/CreateTodo';

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo,
  },
  data() {
    return {
      todos: [{
        title: 'Shop',
        project: 'Need to buy an iPhone',
        date: '2021-03-19',
        done: false,
      }, {
        title: 'Grocery',
        project: 'Suger 1 kg',
        date: '2021-03-4',
        done: false,
      }],
    };
  },
  methods: {
    createTodo(newTodo) {
      this.todos.push(newTodo);
      this.$swal('Success!', 'Item created!', 'success');
    },
  },
};
</script>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
