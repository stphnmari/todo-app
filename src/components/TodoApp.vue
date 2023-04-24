<template>
  <div class="container">
    <h1 class="mt-4 text-center">TODO LIST</h1>
    <div>
      <label for="name"><h3>TASK DESCRIPTION</h3></label>
      <input
        type="text"
        placeholder="Add Task"
        v-model="newTask"
        class="form-control" />
      <label for="date"><h3>TARGET DATE</h3></label>
      <input
        type="date"
        placeholder="Target Date"
        v-model="date"
        class="form-control" />
    </div>
    <button type="button" @click="addTask" class="btn btn-dark"> SAVE </button>
    <input type="checkbox" v-model="checkbox" >
  <div> <label for="checkbox">VIEW ALL COMPLETED TASK</label></div>
  <br>
    <table class="table table-bordered" v-show="checkbox == false">
      <thead>
        <th scope="col" style="width:100px">#</th>
      <th scope="col" style="width:400px">TASKS</th>
      <th scope="col" style="width:500px">TARGET DATE</th>
      <th scope="col" style="width:500px">ACTION</th>
      </thead>
      <tbody>
        <tr v-for="(task, index) in allTask" v-bind:key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ task.description }}</td>
          <td>{{ task.targetDate }}</td>
          <td>
            <div v-show="task.completed == false">
            <button class="btn btn-dark" @click="completeTask(index)">Complete</button>
            <button class="btn btn-danger" @click="deleteTask(task)">Delete</button>
          </div>
          <div v-if="task.completed == true"> Completed task</div>
        </td>
      </tr>
      </tbody>
    </table>
    <table class="table table-bordered" v-show="checkbox == true">
      <thead>
        <th scope="col" style="width:100px">#</th>
      <th scope="col" style="width:400px">TASKS</th>
      <th scope="col" style="width:500px">TARGET DATE</th>
      <th scope="col" style="width:500px">ACTION</th>
      </thead>
      <tbody>
        <tr v-for="(task, index) in allTask" v-bind:key="index" v-show="task.completed">
          <td>{{ index + 1 }}</td>
          <td>{{ task.description }}</td>
          <td>{{ task.targetDate }}</td>
          <td>
            <div v-show="task.completed == false">
            <button class="btn btn-dark" @click="completeTask(index)">Complete</button>
            <button class="btn btn-danger" @click="deleteTask(task)">Delete</button>
            </div>
            <div v-if="task.completed == true"> Completed</div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data: () => ({
    newTask: "",
    newDate: "",
    completed: true,
    checkbox: false,
    allTask: [],
  }),
  methods: {
    addTask() {
      if (!this.newTask || !this.date) {
        return;
      }
    const newTask = {
        description: this.newTask,
        targetDate: this.date,
        completed: false,
      };
      this.allTask.push(newTask);
      this.newTask = "";
      this.date = "";
    },
    completeTask(index) {
      //task.completed = true;
      this.allTask[index].completed = true;
    },
    deleteTask(task) {
      this.allTask.splice(this.allTask.indexOf(task), 1);
    },
  },
};
</script>
