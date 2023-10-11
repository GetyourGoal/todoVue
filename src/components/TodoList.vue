<template>
  <div>
    <h2>To-Do List</h2>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <div>
      <label>Show: </label>
      <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="incomplete">Incomplete</option>
      </select>
    </div>
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button @click="toggleComplete(index)">{{ task.completed ? 'Completed' : 'Incomplete' }}</button>
        <button @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      filter: 'all'
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'completed') {
        return this.tasks.filter(task => task.completed);
      } else if (this.filter === 'incomplete') {
        return this.tasks.filter(task => !task.completed);
      } else {
        return this.tasks;
      }
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
      } else {
        alert('Task title cannot be empty.'); // Display an alert for validation error
      }
    },
    toggleComplete(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: #888;
}

#app {
  font-family: Arial, sans-serif;
  text-align: center;
  max-width: 400px;
  margin: 0 auto;
}

h2 {
  background-color: #333;
  color: #fff;
  padding: 10px;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ccc;
  margin: 5px 0;
  padding: 10px;
  background-color: #f9f9f9;
}

li span {
  flex-grow: 1;
}

button {
  background-color: #d9534f;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  font-size: 14px;
}

select {
  padding: 5px;
}
</style>
