<script setup>
const props = defineProps({
  task: {
    type: Object
  },
})

const emit = defineEmits(['toggle-status', 'delete-task'])

const toggleStatus = () => emit('toggle-status', props.task)
const deleteTask = () => emit('delete-task', props.task)
</script>

<template>
  <li class="task-item">
    <span :class="{ completed: task.completada }">
      {{ task.titulo }} - {{ task.dataCreacio }}
    </span>

    <button @click="toggleStatus">
      {{ task.completada ? 'Descompletar' : 'Completar' }}
    </button>
  
    <button @click="deleteTask">Eliminar</button>
  </li>
</template>
