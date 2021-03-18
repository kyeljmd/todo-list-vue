<template>
  <div>
    <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in todos" :todo.sync="todo" :key="todo"></todo>
  </div>
</template>

<script type = "text/javascript" >
import Todo from './Todo';
export default {
  props: ['todos'],
  components: {
    Todo,
  },
  methods: {
    deleteTodo(todo) {
      this.$swal({
        title: 'Are you sure?',
        text: 'This Item will be permanently deleted!',
        showDenyButton: true,
        showCancelButton: false,
        confirmButtonText: 'Yes, delete it!',
      }).then((result) => {
        /* Read more about isConfirmed, isDenied below */
        if (result.isConfirmed) {
            const todoIndex = this.todos.indexOf(todo);
            this.todos.splice(todoIndex, 1);
            this.$swal('Deleted!', 'Your item has been deleted.', 'success');
        } 
      })
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      this.$swal('Success!', 'Item completed!', 'success');
    },
  },
};
</script>