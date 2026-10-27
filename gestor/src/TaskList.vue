<script setup>
import TaskItem from './TaskItem.vue'

const props = defineProps({
  tasks: {
    type: Array
  },
})

const emit = defineEmits(['toggle-status', 'delete-task'])
</script>

<template>
  <ul v-if="tasks.length">
    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @toggle-status="emit('toggle-status', $event)"
      @delete-task="emit('delete-task', $event)"
    />
  </ul>
  <p v-else>No hay tareas disponibles.</p>
</template>