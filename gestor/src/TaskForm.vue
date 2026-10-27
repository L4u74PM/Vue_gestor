<template>
  <div>
    <label for="task">Nueva tarea:</label>
    <input v-model="nuevaTarea" type="text" id="task" placeholder="Nueva tarea" />
    <button @click="agregarTarea">Agregar</button>
  </div>
</template>

<script setup>

import {ref} from 'vue'
const emit = defineEmits(['add-task'])
const nuevaTarea = ref('')

const agregarTarea = () => {
  const titulo = nuevaTarea.value.trim()

  if (titulo !== '') {
    emit('add-task', {
      titulo,
      dataCreacio: new Date().toISOString().split('T')[0],
      completada: false,
    })
    nuevaTarea.value = ''
  }
}

</script>