<template>
  <div>
    <h1>{{title}}</h1>
    <input type="text" v-model="inputTask" />
    <button @click="addTask">añadir</button>
    <h3>Estás insertando:</h3>
    <h1>{{inputTask}}</h1>
    <ul v-for="task in tasksList" :key="task.id">
      <Task :text="arrText">{{task}}</Task>
    </ul>
  </div>
</template>

<script>
import Task from '../components/Task.vue';

export default {
  data() {
    return {
      i: 0,
      title: '- Task Manager -',
      inputTask: '',
      tasksList: [],
    };
  },
  components: {
    Task,
  },
  methods: {
    addTask() {
      this.tasksList.push(this.inputTask);
    },
  },
};
</script>
