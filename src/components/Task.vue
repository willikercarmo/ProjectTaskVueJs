<template>
  <div>
    <h1 class="display-4 text-center">To-Do List</h1>
    <hr />
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
        <div class="card">
          <div class="card-body">
            <div class="input-group">
              <input
                type="text"
                class="form-control form-control-lg"
                placeholder="Add tak"
                v-model="task"
              />
              <div class="input-group-append">
                <button @click="addTask()" class="btn btn-success btn-lg">
                  Add
                </button>
              </div>
            </div>
            <br />
            <h5 v-if="listTasks.length == 0">There are no task to do</h5>
            {{ listTasks }}

            <ul class="list-group">
              <li
                v-for="(task, index) of listTasks"
                :key="index"
                class="list-group-item d-flex justify-content-between"
              >
                <span class="cursor" v-bind:class="{'text-success': task.status}"
                @click="editTask(task, index)">
                  <i v-bind:class="[task.status ? 'fa-solid fa-circle-check' : 'fa-regular fa-circle']" ></i>
                </span>
                {{ task.name }}
                <span class="text-danger cursor" @click="removeTask(index)">
                  <i class="fas fa-trash-alt"></i>
                </span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  data() {
    return {
      task: "",
      listTasks: [],
    };
  },
  methods: {
    addTask() {
      const task = {
        name: this.task,
        status: false,
      };
      this.listTasks.push(task);
      this.task = "";
    },
    removeTask(index) {
      this.listTasks.splice(index, 1);
    },
    editTask(task, index) {
      this.listTasks[index].status = !task.status;
    },
  },
};
</script>

<style scoped>
.cursor {
  cursor: pointer;
}
</style>
