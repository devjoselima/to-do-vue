<script setup>
    const props = defineProps(['tasks']);

</script>

<template>
    <ul class="list-group mt-4">
    <li class="list-group-item" v-for="task in props.tasks">
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
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }

</style>