<template>
  <Title :brand="brand" :proprietor="proprietor" :contact_lines="contact_lines"/>
  <ToDoList :todos="todos" v-on:display-form="requestForm($event)"/>
  <div class="task-form">
    <TaskCreate :todos="todos" 
      v-on:TaskCreate="createTask($event)" 
      v-on:hide-create-form="hideForm" 
      v-if="formToShow == 'Create'">
    </TaskCreate>
    <TaskUpdate :todos="todos" 
      :taskID="taskID" 
      v-on:TaskUpdate="updateTask($event)" 
      v-on:hide-update-form="hideForm" 
      v-if="formToShow == 'Update'">
    </TaskUpdate>
    <TaskDelete :todos="todos" 
      :taskID="taskID" 
      v-on:TaskDelete="deleteTask($event)" 
      v-on:hide-delete-form="hideForm" 
      v-if="formToShow == 'Delete'">
    </TaskDelete>
</div>
</template>

<script>
import Title from './components/Title.vue';
import ToDoList from './components/ToDoList.vue';
import TaskCreate from './components/TaskCreate.vue';
import TaskUpdate from './components/TaskUpdate.vue';
import TaskDelete from './components/TaskDelete.vue';

export default {
  name: 'App',
  Debug: 1,
  components: { Title, ToDoList, TaskCreate, TaskUpdate, TaskDelete },

  data() {
    return {
      Name: "Root",
      Debug: 2,
      formToShow: "",
      taskID: -7,
      brand: 'Plain Jane CRUD',
      proprietor: 'Bugs Bunny',
      contact_lines: [
        "456 Park Street",
        "Toronto, ON",
        "H0H 0H0",
        "416 555 1212 [Phone]",
        "905 555 1212 [Fax]",
        "info@example.com"
      ],
      todos: [
        { id: 1, description: "Get a handle on props", priority: "High", status: "Completed" },
        { id: 2, description: "Write a CRUD application in Vue", priority: "High", status: "Completed" }, 
        { id: 3, description: "Implement a live Vue app", priority: "High", status: "Pending" },
        { id: 4, description: "Test CRUD application with Dusk", priority: "High", status: "Pending" },
        { id: 5, description: "Integrate Vuetify with Vue", priority: "High", status: "Pending" },
        { id: 6, description: "Combine Vue, Vuetify and Laravel", priority: "High", status: "Pending" },
        { id: 7, description: "Integrate Vuelidate with Vue", priority: "Low", status: "Pending" },
        { id: 8, description: "Store/update on database", priority: "Medium", status: "Pending" },
        { id: 9, description: "Finish Project A", priority: "Low", status: "Pending" },
        { id: 10, description: "Finish Project B", priority: "Low", status: "Pending" },
      ],
    }
  },
  methods: {
    requestForm(object) {
      if (this.Debug >= 1) console.log(this.Name + ".requestForm() - formName: " + object.form + "; index: " + object.taskID);
      this.formToShow = object.form;
      this.taskID = object.taskID;
      if (this.Debug >= 2) console.log(this.Name + ".requestForm() - taskID saved in parent: " + this.taskID);
    },
    createTask(newTask) {
      if (this.Debug >= 1) console.log(this.Name + ".createTask() - new Task - description: " + newTask.description + "; priority: " + newTask.priority + "; status: " + newTask.status);
      /* Loop thru the array to get highest current taskID from the existing data. */
      var highestTaskID = -1;
      for (let todo of this.todos) {
        if (todo.id > highestTaskID) highestTaskID = todo.id;
      }
      if (this.Debug >= 2) console.log(this.Name + ".createTask() - highest existing task ID: " + highestTaskID);
      var newTaskID = highestTaskID + 1; /* Calculate the ID of the new task. */
      var taskToCreate = { id: newTaskID, description: newTask.description,  priority: newTask.priority, status: newTask.status };
      this.todos[this.todos.length] = taskToCreate; //create the new task 
      this.hideForm();
    },
    updateTask(updatedTask) {
      if (this.Debug >= 1) console.log(this.Name + ".updateTask() - updated Task - id: " + updatedTask.id + "; description: " + updatedTask.description + "; priority: " + updatedTask.priority + "; status: " + updatedTask.status);
      var positionOfTaskBeingUpdated = this.todos.findIndex(obj => obj.id == updatedTask.id); //find position of task to be updated
      if (this.Debug >= 2) console.log(this.Name + ".updateTask() - position of task being updated: " + positionOfTaskBeingUpdated);
      this.todos.splice(positionOfTaskBeingUpdated, 1, updatedTask) //replace old version of task with new one
      this.hideForm();
    },
    deleteTask(taskIDToBeDeleted) {
      if (this.Debug >= 1) console.log(this.Name + ".deleteTask() - taskIDToBeDeleted - " + taskIDToBeDeleted);
      var positionOfTaskBeingDeleted = this.todos.findIndex(obj => obj.id == taskIDToBeDeleted);
      if (this.Debug >= 2) console.log(this.Name + ".deleteTask() - position of task being deleted: " + positionOfTaskBeingDeleted);
      this.todos.splice(positionOfTaskBeingDeleted, 1); //delete the task
      this.hideForm();
    },
    hideForm() {
      this.formToShow = "";
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  /* -moz-osx-font-smoothing: grayscale; */
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
.ToDoList {
  width: 50%;
  float: left;
}
.task-form {
  width: 50%;
  float: right;
}
</style>