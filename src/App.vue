<script setup>
  import { reactive } from 'vue';
  import Header from './components/Header.vue';
  import Formulario from './components/Form.vue';
  import Tasks from './components/Tasks.vue';

  const state = reactive({
    filter: 'todas',
    tempTask: '',
    tasks: [
      {
        title: 'Estudar ES6',
        isDone: false,
      },
      {
        title: 'Estudar SASS',
        isDone: false,
      },
      {
        title: 'Estudar React',
        isDone: true,
      },
    ]
  })

  const getPendingTasks = () => {
    return state.tasks.filter( task => !task.isDone)
  }
  const getFinishedTasks = () => {
    return state.tasks.filter( task => task.isDone)
  }

  const getFilterTasks = () => {
    const { filter } = state;

    switch (filter) {
      case 'pendentes':
        return getPendingTasks();
      case 'finalizadas':
        return getFinishedTasks();
      default:
        return state.tasks;
    }
  }

  const setTask = () => {
    const newTask = {
      title: state.tempTask,
      isDone: false,
    }
    state.tasks.push(newTask)
    state.tempTask = '';
  }
</script>

<template>
  <div class="container">
    <Header 
      :pendingTasks="getPendingTasks().length" 
    />
    <Formulario 
      :changeFilter="event => state.filter = event.target.value"
      :tempTask="state.tempTask" 
      :editTempTask="event => state.tempTask = event.target.value" 
      :setTask="setTask"
    />
    <Tasks
      :tasks="getFilterTasks()"
    />
  </div>
</template>

<style scoped>
</style>
