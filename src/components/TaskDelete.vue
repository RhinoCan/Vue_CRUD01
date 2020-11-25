<template>
<div class="task-form">
  <h1>Delete Task</h1>
  <form>
    <label for="taskID">Task ID: </label>{{ taskID }}<br><br>
    <label for="description">Task Description: </label>
    <input type="text" id="description" v-model="description" disabled><br><br>
    <label for="priority">Task Priority: </label>
    <select id="priority" v-model="priority" disabled>
    <option disabled value="">Please select one</option>
    <option>Low</option>
    <option>Medium</option>
    <option>High</option>
    </select><br><br>
    <label for="status">Task Status: </label>
    <select id="status" v-model="status" disabled>
    <option disabled value="">Please select one</option>
    <option>Pending</option>
    <option>Completed</option>
    </select><br><br>
    <button type="cancel" @click="cancelDelete">Cancel</button>
    <button type="submit" @click="deleteTask">Delete Task</button>
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
      Name: "TaskDelete",
      Debug: 2,
      description: '',
      priority: '', 
      status: '',
      errors: [],
    }
  },
  computed: {
  },
  methods: {
    cancelDelete() {
      this.$emit("hide-delete-form");
      return;
    },
    deleteTask(event) {
      if (this.Debug >= 1) console.log(this.Name + ".deleteTask() - event: " + event);
      if (this.Debug >= 2) console.log(this.Name + ".deleteTask() - number of tasks before deleting: " + this.todos.length);

      event.preventDefault();
      
      /* Determine the ID of the task that is to be deleted. Emit it to the parent so that it can delete
      that task from the todos data structure. */
      var taskIDToDelete = this.taskID;
      if (this.Debug >= 2) console.log(this.Name + ".deleteTask() - taskIDToDelete: " + taskIDToDelete);
      this.$emit(this.Name, taskIDToDelete);

      this.description = "";
      this.priority = "";
      this.status = "";
    },
    
  }, 
  created()  {
    if (this.Debug >= 1) console.log("Created " + this.Name);
    if (this.Debug >= 2) console.log(this.Name + ".created() - taskID: " + this.taskID);
    //Search the array of objects to find the one object whose taskID equals the one passed in the taskID prop.
    let targetTask = this.todos.find(targetTask => targetTask.id == this.taskID);
    if (this.Debug >= 2) console.log(this.Name + ".created() - description: " + targetTask.description );
    if (this.Debug >= 2) console.log(this.Name + ".created() - priority: " + targetTask.priority );
    if (this.Debug >= 2) console.log(this.Name + ".created() - status: " + targetTask.status );
    this.description = targetTask.description;
    this.priority = targetTask.priority;
    this.status = targetTask.status;
  },
}
</script>

<style scoped>
form {
  padding: 20px;
  border: 3px solid black;
}
</style>
