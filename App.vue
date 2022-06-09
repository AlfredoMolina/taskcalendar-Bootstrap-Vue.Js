<template>
  <div class="container">
    <h2 class="text-center">Task Calnedar </h2>

    <div id="d-flex">
      <input v-model="task" type="text" placeholder="Enter" class="form-control">
      <br>
      <button @click="submitTask" class="btn btn-primary rounded-6">Submit</button>
    </div>
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td><span @click="changeStatus(index)" class="pointer">{{ task.status }}</span></td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>


<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      task: '',
      editedTask: null,
      availableSatuses: ['upcoming', 'in-progress','finished'],
      tasks: [
        {
          name: 'Code Review/Testing',
          status: 'in-progress'
        },
        {
          name: 'Deploy App V.1',
          status: 'upcoming'
        }
      ]
    }
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;
      if(this.editedTask === null){
    
      this.tasks.push({
        name: this.task,
        status: 'upcoming'
      });
      }else{
      this.tasks[this.editedTask].name = this.task;
      this.editedTask = null;
      }
      this.task = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index){
   let newIndex = this.availableSatuses.indexOf(this.tasks[index].status);
   if(++newIndex > 2) newIndex = 0;
   this.tasks[index].status = this.availableSatuses[newIndex];

    },
  }
}
</script>

<style>
* {
  cursor: pointer;
}
</style>