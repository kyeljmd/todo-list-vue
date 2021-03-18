<template>
  <div class='col-sm-12'>
    <b-card v-show="!isEditing" class="mb-4">
      <div class="row">
      <div class='col-sm-3'>
          {{ todo.title }}
      </div>
      <div class='col-sm-3'>
          {{ todo.project }}
      </div>
      <div class='col-sm-3'>
         Due date: {{ todo.date }}
      </div>
      <div class='col-sm-3'>
          <span class='' v-on:click="showForm">
        <b-icon icon="pencil-square" aria-hidden="true"></b-icon>
        </span>
        <span class='' v-on:click="deleteTodo(todo)">
        <b-icon icon="trash-fill" aria-hidden="true"></b-icon>
        </span>
      </div>
      </div>
    </b-card>
       <b-alert v-model="showDismissibleAlert" variant="danger" dismissible>
        All fields are required.
    </b-alert>
    <b-card  v-show="isEditing" class="mb-4">
      <div class='row'>
        <div class='col-sm-6'>
          <b-form-group>
            <b-form-input  size="sm" required v-model="todo.title"  placeholder="Enter name"></b-form-input>
            </b-form-group>
        </div>
           <div class='col-sm-6'>
            <b-form-group>
            <b-form-datepicker  size="sm" required v-model="todo.date"  placeholder="Select due date"></b-form-datepicker>
            </b-form-group>
        </div>
        <div class='col-sm-12'>
            <b-form-group>
            <b-form-textarea size="sm" required v-model="todo.project"  placeholder="Enter description"  rows="3" max-rows="6"></b-form-textarea>
            </b-form-group>
        </div>
        <div class='col-sm-2'>
            <b-button variant="success" v-on:click="hideForm(todo)">Save & Close</b-button>
        </div>
      </div>
   </b-card>
  </div>
</template>

<script type="text/javascript">
  export default {
    props: ['todo'],
    data() {
      return {
        isEditing: false,
        showDismissibleAlert: false
      };
    },
    methods: {
      completeTodo(todo) {
        this.$emit('complete-todo', todo);
      },
      deleteTodo(todo) {
        this.$emit('delete-todo', todo);
      },
      showForm() {
        this.isEditing = true;
      },
      hideForm(todo) {
        this.showDismissibleAlert = false
        if(todo.title === '' || todo.date === '' || todo.project === ''){
          this.showDismissibleAlert = true
        }else{
          this.isEditing = false;
        }
      },
    },
  };
</script>
