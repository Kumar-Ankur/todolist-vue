<template>
  <div>
    <div class="row">
      <li class="list-group-item listStyle">
        <div class="custom-control custom-checkbox">
          <input type="checkbox" class="custom-control-input" id="check1" v-model="taskCheck" />
          <label class="custom-control-label" for="check1">
            <slot></slot>
          </label>
        </div>
      </li>
    </div>

    <div class="row" v-if="taskCheck">
      <button
        type="button"
        class="btn btn-primary"
        data-toggle="modal"
        data-target="#myModal"
        @click="isEditMode=true"
      >Edit Task</button>
      <button
        type="button"
        class="btn btn-danger"
        data-toggle="modal"
        data-target="#deleteModal"
        @click="isDeleteMode=true"
      >Delete Task</button>
    </div>

    <div v-if="isEditMode">
      <div class="modal" id="myModal" :style="{ display: 'block'}">
        <div class="modal-dialog">
          <div class="modal-content">
            <!-- Modal Header -->
            <div class="modal-header">
              <h4 class="modal-title">Edit Task</h4>
              <button
                type="button"
                class="close"
                data-dismiss="modal"
                @click="isEditMode=false"
              >&times;</button>
            </div>

            <!-- Modal body -->
            <div class="modal-body">
              <form>
                <div class="row">
                  <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <div class="form-group">
                      <label for="task">Edit Task</label>
                      <input type="text" id="task" class="form-control" v-model="taskName" />
                    </div>
                    <div class="btn btn-success" @click.prevent="editTask">Edit Task</div>
                  </div>
                </div>
              </form>
            </div>

            <!-- Modal footer -->
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-danger"
                data-dismiss="modal"
                @click="isEditMode=false"
              >Close</button>
            </div>
          </div>
        </div>
      </div>
    </div>

          <div v-if="isDeleteMode">
        <div class="modal" id="deleteModal" :style="{ display: 'block'}">
          <div class="modal-dialog">
            <div class="modal-content">
              <!-- Modal Header -->
              <div class="modal-header">
                <h4 class="modal-title">Delete Task</h4>
                <button
                  type="button"
                  class="close"
                  data-dismiss="modal"
                  @click="isDeleteMode=false"
                >&times;</button>
              </div>

              <!-- Modal body -->
              <div class="modal-body">
                <span>Are you sure you want to delete this task? Once Deleted, task cannot be reversed.</span>
              </div>

              <!-- Modal footer -->
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-danger"
                  data-dismiss="modal"
                  @click="deleteTask"
                >Delete</button>
              </div>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import { eventBus } from "../main";
export default {
  props: ["index", "task"],
  data() {
    return {
      taskCheck: false,
      isEditMode: false,
      isDeleteMode: false,
      taskName: this.task
    };
  },
  methods: {
    deleteTask() {
      eventBus.$emit("removeTask", this.index);
    },
    editTask() {
      const payload = {
        index: this.index,
        name: this.taskName
      };
      eventBus.$emit("editTask", payload);
      this.isEditMode = false;
    }
  }
};
</script>

<style scoped>
.listStyle {
  font-size: 15px;
  color: #6e6e6e;
  margin-bottom: 2rem;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
</style>