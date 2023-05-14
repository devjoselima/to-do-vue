<script setup>
    const props = defineProps(['setTask', 'tempTask', 'changeFilter', 'editTempTask']);
</script>

<template>
    <form @submit.prevent="props.setTask">
    <div class="row">

      <div class="col">
        <input 
          :value="props.tempTask"
          @change="props.editTempTask"
          required 
          type="text" 
          placeholder="Digite aqui a tarefa" 
          class="form-control"
        />
      </div>

      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>

      <div class="col-md-2">
        <select @change="props.changeFilter" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>