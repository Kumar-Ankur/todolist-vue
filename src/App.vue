<template>
  <div class="container">
    <app-header></app-header>
    <app-add-new-task @addNewTask="addNewTask"></app-add-new-task>
    <hr />
    <app-list-item :tasks="tasks"></app-list-item>

    <div class="row">
      <div class="col-sm-12 text-center">
        <div class="alert alert-success" v-if="isEdit">Info: Task has been edited successfully!!</div>
      </div>
    </div>

    <div class="row">
      <div class="col-sm-12 text-center">
        <div class="alert alert-danger" v-if="isDelete">Info: Task has been deleted successfully!!</div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./Components/Header.vue";
import AddNewTask from "./Components/AddNewTask.vue";
import ListItem from "./Components/listItem.vue";
import { eventBus } from "./main";
export default {
  components: {
    appHeader: Header,
    appAddNewTask: AddNewTask,
    appListItem: ListItem
  },
  data: function() {
    return {
      tasks: [],
      isEdit: false,
      isDelete: false
    };
  },
  methods: {
    addNewTask(task) {
      this.tasks.unshift(task);
    }
  },
  watch: {
    isEdit: function(val) {
      setTimeout(() => {
        this.isEdit=false
      }, 3000);
    },
    isDelete: function(val) {
      setTimeout(() => {
        this.isDelete = false;
      }, 3000);
    }
  },
  created: function() {
    eventBus.$on("removeTask", index => {
      this.tasks.splice(index, 1);
      this.isDelete = true;
    });
    eventBus.$on("editTask", payload => {
      const { index, name } = payload;
      this.tasks.splice(index, 1);
      this.tasks.unshift(name);
      this.isEdit=true
    });
  }
};
</script>

<style>
</style>
