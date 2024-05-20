<template>
    <div>
      <h1>To-Do-List</h1>
      <input v-model="newTask" placeholder="Agregar nueva tarea" />
      <button @click="addTask">Agregar</button>
      <ul>
        <task-item
          v-for="(task, index) in tasks"
          :key="index"
          :task="task"
          @remove="removeTask(index)"
          @toggle="toggleTask(index)"
        ></task-item>
      </ul>
    </div>
  </template>
  
  <script>
  import TaskItem from './TaskItem.vue';
  
  export default {
    components: { TaskItem },
    data() {
      return {
        newTask: '',
        tasks: []
      };
    },
    methods: {
      addTask() {
        if (this.newTask.trim() !== '') {
          this.tasks.push({ text: this.newTask, completed: false });
          this.newTask = '';
          this.saveTasks();
        }
      },
      removeTask(index) {
        this.tasks.splice(index, 1);
        this.saveTasks();
      },
      toggleTask(index) {
        this.tasks[index].completed = !this.tasks[index].completed;
        this.saveTasks();
      },
      saveTasks() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      },
      loadTasks() {
        const savedTasks = localStorage.getItem('tasks');
        if (savedTasks) {
          this.tasks = JSON.parse(savedTasks);
        }
      }
    },
    created() {
      this.loadTasks();
    }
  };
  </script>
  
<style scoped>
  
.task-list {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 10px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.input-group {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

input {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

button {
  padding: 10px 20px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #218838;
}

ul {
  list-style-type: none;
  padding: 0;
}
</style> 
