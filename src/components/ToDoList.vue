<template>
<div class="ToDoList">
  <h1>To Do List</h1>
  <table class="task-list">
    <tr>
      <td><button @click="displayForm({form:'Create', taskID: -1})">Create a New Task</button></td>
      <!-- <td><button @click="displayForm({form: 'Hide', taskID: -1})">Hide Task Forms</button></td> -->
    </tr>
  </table>
  <table class="task-list">
    <tr><th>Task ID</th><th>Description</th><th>Priority</th><th>Status</th><th>Update</th><th>Delete</th></tr>
    <tr v-for="todo in todos" :key="todo.id">
      <!-- <td>
        <img v-if="todo.status" class="check" src="../assets/images/check.svg"/>
        <img v-else class="cross" src="../assets/images/cross.svg"/>
      </td> -->
      <td class="numeric-column">{{ todo.id }}</td><!-- show task ID -->
      <td>{{ todo.description }}</td><!-- show description -->
      <td>{{ todo.priority }}</td><!-- show priority -->
      <td>{{ todo.status }}</td><!-- show status -->
      <td><button @click="displayForm({form: 'Update', taskID: todo.id})">Update this Task</button></td><!-- show edit icon -->
      <td><button @click="displayForm({form: 'Delete', taskID: todo.id})">Delete this Task</button></td><!-- show delete icon -->
    </tr>
  </table>
  <p class="task-summary">Completed items: {{ completed }};  pending items {{ pending }}.</p>
</div>
</template>

<script>
export default {
  props: {
        todos: { type: Array, required: false, default: () => [{ id: 0, description: "No Tasks Provided", priority: "High", status: "Pending" }] }
      },
  data() {
    return {
      Name: "ToDoList",
      Debug: true,
      choice: { form: "", taskID: -99 },
    }
  },
  computed: {
    completed() {
      /* Find the tasks that have a completed status and put them in a new array. 
      Count the tasks in the new array and return that. */
      let completedTasks = this.todos.filter(obj => obj.status == "Completed");
      return completedTasks.length;
    },
    pending() {
  /* Find the tasks that have a pending status and put them in a new array. 
      Count the tasks in the new array and return that. */
      let pendingTasks = this.todos.filter(obj => obj.status == "Pending");
      return pendingTasks.length;
    }
  },
  methods: {
      displayForm(object) {
        if (this.Debug) console.log("displayForm - formName: " + object.form + "; index: " + object.taskID);
        this.choice.form = object.form;
        this.choice.taskID = object.taskID;
        this.$emit('display-form', this.choice);
    }
  },
  created()  {
    if (this.Debug) console.log("Created " + this.Name);
  }
}
</script>

<style scoped>
.check, .cross {
  width: 30px;
}
ul {
  list-style-type: none;
}
li {
  font-size: 24px;
}
table.task-list {
  margin: 0 auto;
  text-align: left;
  border: 3px solid black;
  border-collapse: collapse;
  margin-bottom: 15px;
}
tr, th, td {
  border: 1px solid black;
  padding: 10px;
}
.numeric-column {
  text-align: right;
}
.task-summary {
  padding-top: 15px;
  margin: 0 auto;
}

</style>
