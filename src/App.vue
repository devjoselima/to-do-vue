<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded text-center">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getPendingTasks().length }} tarefas pendentes
      </p>
    </header>

    <form @submit.prevent="setTask">
    <div class="row">

      <div class="col">
        <input 
          :value="state.tempTask"
          required 
          type="text" 
          @change="event => state.tempTask = event.target.value"
          placeholder="Digite aqui a tarefa" 
          class="form-control"
        />
      </div>

      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>

      <div class="col-md-2">
        <select @change="event => state.filter = event.target.value" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>

  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="task in getFilterTasks()">
      <input 
        type="checkbox" 
        :checked="task.isDone" 
        :id="task.title"
        @change = 'event => task.isDone = event.target.checked'
      />

      <label :class="{ done: task.isDone }" class="ms-3" :for="task.title">   
        {{ task.title }}
      </label>
    </li>
  </ul>
  </div>
 
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }

</style>
