<template>
  <div class="container">
    <!-- heading -->
    <h2 class="text-center mt-5 mb-5 heading">*{Vue Todo App}*</h2>
    <!-- Inputs -->
    <div class="mb-5 d-flex justify-content-around">
      <input
        v-model="task"
        type="text"
        placeholder="Enter a task"
        class="task-input"
      />
      <button @click="addTask" class="btn add-task">
        <span class="fa fa-plus"></span> Add
      </button>
    </div>
    <!-- Task Table -->
    <table class="table table-bordered">
      <thead>
        <tr>
          <th class="text-center" scope="col">Task</th>
          <th class="text-center" scope="col">
            Status (<span style="color: #42b883">click</span> to change)
          </th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td style="width: 40%">
            <span :class="{ finished: task.status === 'Finished' }">{{
              task.name
            }}</span>
          </td>
          <td class="text-center" style="width: 30%; font-weight: 500">
            <span
              @click="changeStatus(index)"
              style="cursor: pointer"
              :class="{
                'text-danger': task.status === 'To-do',
                'text-warning': task.status === 'In-progress',
                'text-success': task.status === 'Finished',
              }"
              >{{ task.status }}</span
            >
          </td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span
                class="fa fa-pen"
                style="cursor: pointer; color: #2980b9"
              ></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span
                class="fa fa-trash"
                style="cursor: pointer; color: #e74c3c"
              ></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: "",
      editedTask: null,
      availableStatus: ["To-do", "In-progress", "Finished"],
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.task.length <= 3)
        return alert("Enter a valid task , more than 3 characters");
      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "To-do",
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index) {
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatus[newIndex];
    },
  },
};
</script>

<style scoped>
.finished {
  text-decoration: line-through;
}
.task-input {
  width: 60%;

  caret-color: #42b883;
  padding: 10px;
  border: none;
  border-radius: 6px;
}
.task-input:focus {
  outline: none;
  border: none;
}
.add-task {
  background-color: #213547;
  width: 15%;
  color: #e5e5e5;
  transition: all 0.3s ease-in-out;
}
.add-task:hover {
  background-color: #213547;
  color: #42b883;
}
</style>
