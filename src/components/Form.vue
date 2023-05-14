<script setup>
    const props = defineProps(['setTask', 'tempTask', 'changeFilter', 'editTempTask']);
</script>

<template>
    <form @submit.prevent="props.setTask">
      <div class="row d-flex justify-content-between">
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
        <div class="col-4">
            <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
      </div>

      <div class="row mt-2"> 
        <div class="col-md-4">
          <select @change="props.changeFilter" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>

        
      </div>
    </form>
</template>