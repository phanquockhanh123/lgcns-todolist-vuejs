<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do List</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input type="text" placeholder="New Task" v-model="newTask" @keyup.enter = "addNewTask"/>
        <button @click.prevent="addNewTask"><i class="fas fa-plus"></i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <task-item v-bind:task="task" v-for="(task, index) in tasks" :key="task.id" @remove="removeTask(index)" @complete="completeTask(task)"></task-item>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click.prevent="clearCompletedTask">Clear completed</button>
        <button @click.prevent="clearAll">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ incomplete }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from './Task-Item.vue';

export default {
  name: "Task",
  props: ['tasks'],
  data: function() {
    return {
      newTask: ''
    };
  },
  components: {
    TaskItem
  },
  methods: {
    clearAll() {
      this.tasks = [];
    },
    isCompleted(task) {
      return task.completed;
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    clearCompletedTask() {
      this.tasks = this.tasks.filter(this.inProgress);
    },
    addNewTask: function(e) {
      e.preventDefault();

      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          completed: false
        })
        this.newTask = "";
      }
    },
    removeTask(i) {
      this.tasks.splice(i, 1);
    },
    completeTask(task) {
      task.completed = !task.completed;
    }
  },
  computed: {
    incomplete() {
      return this.tasks.filter(this.inProgress).length;
    }
  }
};
</script>
