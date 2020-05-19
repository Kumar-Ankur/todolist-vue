<template>
  <form>
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <div class="form-group">
          <label for="task">Add Task</label>
          <input type="text" id="task" class="form-control" v-model="newTask" />
        </div>
        <div class="btn btn-success" @click.prevent="handleNewTask">Add Task</div>
      </div>
    </div>
  </form>
</template>
<script>
export default {
  data: function() {
    return {
      newTask: ""
    };
  },
  methods: {
    handleNewTask() {
      if (this.newTask.length > 0) {
        this.$emit("addNewTask", this.newTask);
        this.newTask = ''
      }
    }
  }
};
</script>
<style scoped>
</style>