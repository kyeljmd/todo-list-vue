<template>
  <div class='col-sm-12'>
      <b-alert v-model="showDismissibleAlert" variant="danger" dismissible>
        All fields are required.
    </b-alert>
    <b-button variant="success"  v-on:click="openForm" v-show="!isCreating">Add New</b-button>

      <b-card  v-show="isCreating" class="mb-4">
      <div class='row'>
        <div class='col-sm-6'>
              <b-form-group>
            <b-form-input id="input-" size="sm" v-model="titleText"  placeholder="Enter name"></b-form-input>
              </b-form-group>
        </div>
        <div class='col-sm-6'>
            <b-form-group>
            <b-form-datepicker id="input-11" size="sm" v-model="projectDate"  placeholder="Select due date"></b-form-datepicker>
            </b-form-group>
        </div>
        <div class='col-sm-12'>
                   <b-form-group>
            <b-form-textarea id="input-1" size="sm" v-model="projectText"  placeholder="Enter description"  rows="3" max-rows="6"></b-form-textarea>
            </b-form-group>
        </div>
        <div class='col-sm-2'>
            <b-button variant="success" v-on:click="sendForm()" class="mr-2">Save</b-button>
            <b-button variant="dark" v-on:click="closeForm">Cancel</b-button>
        </div>
      </div>
   </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titleText: '',
      projectText: '',
      projectDate: '',
      isCreating: false,
      showDismissibleAlert: false
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.titleText = '';
      this.projectText = '';
      this.projectDate = '';
      this.isCreating = false;
    },
    sendForm() {
      this.showDismissibleAlert = false
      if (this.titleText.length > 0 && this.projectText.length > 0 && this.projectDate.length > 0) {
        const title = this.titleText;
        const project = this.projectText;
        const date = this.projectDate;
        this.$emit('create-todo', {
          title,
          project,
          date,
          done: false,
        });
        this.titleText = '';
        this.projectText = '';
        this.projectDate = '';
        this.isCreating = false;
      }else{
        this.showDismissibleAlert = true
      }
    },
  },
};
</script>
