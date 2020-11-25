<template>
<div class="task-form">
  <h1>Update Task</h1>
  <div v-if="errors.length">
    <p>Please correct the following errors:</p>
    <ul>
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
  </div>
  <form @submit="updateTask">
    <label for="taskID">Task ID: </label>{{ taskID }}<br><br>
    <label for="description">Task Description: </label><input type="text" id="description" v-model="description"><br><br>
    <label for="priority">Task Priority: </label><select id="priority" v-model="priority">
    <option disabled value="">Please select one</option>
    <option>Low</option>
    <option>Medium</option>
    <option>High</option>
    </select><br><br>
    <label for="status">Task Status: </label><select id="status" v-model="status">
    <option disabled value="">Please select one</option>
    <option>Pending</option>
    <option>Completed</option>
    </select><br><br>
    <button type="cancel" @click="cancelUpdate">Cancel</button>
    <button type="submit" @click="updateTask">Update Task</button>
  </form>
</div>

</template>

<script>
export default {
  props: {
        todos: { type: Array, required: false, default: () => [{ id: 0, task: "No Tasks Provided", priority: "High", status: "Pending" }] },
        taskID: { type: Number, required: true }
      },
  data() {
    return {
      Name: "TaskUpdate",
      Debug: 2,
      tID: '',
      description: '',
      priority: '',
      status: '',
      errors: [],
    }
  },
  computed: {
  },
  methods: {
    cancelEdit() {
      this.$emit("hide-update-form");
      return;
    },
    updateTask(event) {
      if (this.Debug >= 1) console.log(this.Name + ".updateTask() - event: " + event);
      if (this.Debug >= 2) console.log(this.Name + ".updateTask() - number of tasks before updating: " + this.todos.length);
      this.errors.splice(0, this.errors.length); //remove all elements previously put in this array
      if (this.description.length == 0) {
        this.errors.push("Task description must be supplied.");
      }
      if (!this.priority) {
        this.errors.push("Task priority must be supplied.");
      }
      if (!this.status) {
        this.errors.push("Task status must be supplied.");
      }

      event.preventDefault();

      if (this.errors.length == 0) {

        /* Create an updated task containing the revised details of the task. Emit it to the parent so that it 
        can update the todos data structure. */
        if (this.Debug >= 2) console.log(this.Name + ".updateTask() - Variables - TaskID: " + this.taskID + "; description: " + this.description + "; priority: " + this.priority + "; status: " + this.status);
        var updatedTask = {id: this.taskID, description: this.description, priority: this.priority, status: this.status};
        if (this.Debug >= 2) console.log(this.Name + ".updateTask() - Updated task - TaskID: " + updatedTask.id + "; description: " + updatedTask.description + "; priority: " + updatedTask.priority + "; status: " + updatedTask.status);
        this.$emit(this.Name, updatedTask);

        /* Clear out the form fields. */
        this.description = "";
        this.priority = "";
        this.status = "";
      }
    }
  }, 
  created()  {
    if (this.Debug >= 1) console.log("Created " + this.Name);
    if (this.Debug >= 2) console.log(this.Name + ".created() - taskID: " + this.taskID);
    // this.tID = this.taskID;
    //Search the array of objects to find the one object whose taskID equals the one passed in the taskID prop.
    let targetTask = this.todos.find(obj => obj.id == this.taskID);
    if (this.Debug >= 2) console.log(this.Name + ".created() - description: " + targetTask.description );
    if (this.Debug >= 2) console.log(this.Name + ".created() - priority: " + targetTask.priority );
    if (this.Debug >= 2) console.log(this.Name + ".created() - status: " + targetTask.status );
    this.description = targetTask.description;
    this.priority = targetTask.priority;
    this.status = targetTask.status;
  }
}
</script>

<style scoped>
form {
  padding: 20px;
  border: 3px solid black;
}
</style>
