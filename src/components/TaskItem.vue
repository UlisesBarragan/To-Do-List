<template>
    <li>
      <input type="checkbox" :checked="task.completed" @change="toggleTask" />
      <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.text }}</span>
      <button @click="$emit('remove')">X</button>
    </li>
  </template>
  
  <script>
  export default {
    props: ['task'],
    methods: {
      toggleTask() {
        this.$emit('toggle');
      }
    }
  };
  </script>
  
  <style scoped>
  .task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ddd;
    background-color: #fff;
    transition: background-color 0.3s;
  }
  
  .task-item:last-child {
    border-bottom: none;
  }
  
  input[type="checkbox"] {
    margin-right: 10px;
  }
  
  button {
    background-color: #dc3545;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 10px; 
    padding: 3px 8px;
    cursor: pointer;
    margin-left: 10px;
  }
  
  button:hover {
    background-color: #c82333;
  }
  
  .completed {
    text-decoration: line-through;
    color: #6c757d;
  }
  
  .task-item:hover {
    background-color: #f8f9fa;
  }
  </style>
  