<template>
<div class="task-form">
  <h1>Create Task</h1>
  <div v-if="errors.length">
    <p>Please correct the following errors:</p>
    <ul>
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
  </div>
  <form @submit="createTask">
    <label for="description">Task Description: </label>
    <input type="text" id="description" v-model="description"><br><br>
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
    <button type="cancel" @click="cancelCreate">Cancel</button>
    <button type="submit" @click="createTask">Create Task</button>
  </form>
</div>

</template>

<script>
export default {
  props: {
        todos: { type: Array, required: false, default: () => [{ id: 0, task: "No Tasks Provided", priority: "High", status: "Pending" }] }
      },
  data() {
    return {
      Name: "TaskCreate",
      Debug: 2,
      description: '',
      status: '',
      priority: '',
      errors: [],
    }
  },
  computed: {
  },
  methods: {
    cancelCreate() {
      this.$emit("hide-create-form");
      return;
    },
    createTask(event) {
      if (this.Debug >= 1) console.log(this.Name + ".createTask() - event: " + event);
      if (this.Debug >= 2) console.log(this.Name + ".createTask() - number of tasks before creating: " + this.todos.length);
      this.errors.splice(0, this.errors.length); //remove all elements previously put in the errors array
      if (this.description.length == 0) {
        this.errors.push("Task description must be supplied.");
      }
      if (!this.status) {
        this.errors.push("Task status must be supplied.");
      }
      if (!this.priority) {
        this.errors.push("Task priority must be supplied.");
      }

      event.preventDefault();

      if (this.errors.length == 0) {
        
        /* Create a new task containing the details of the task. Emit it to the parent so that it can update
        the todos data structure. */
        if (this.Debug >= 2) console.log(this.Name + ".createTask() - Variables - TaskID: " + this.id + "; description: " + this.description + "; priority: " + this.priority + "; status: " + this.status);
        var newTask = {id: this.todos.length+1, description: this.description, priority: this.priority, status: this.status};
        if (this.Debug >= 2) console.log(this.Name + ".createTask() - New task - TaskID: " + newTask.id + "; description: " + newTask.description + "; priority: " + newTask.priority + "; status: " + newTask.status);
        this.$emit(this.Name, newTask);

        /* Clear out the form fields. */
        this.description = "";
        this.status = "";
        this.priority = "";
      }
    }
  }, 
  created()  {
    if (this.Debug >= 1) console.log("Created " + this.Name);
  }
}
</script>

<style scoped>
form {
  padding: 20px;
  border: 3px solid black;
}
</style>
