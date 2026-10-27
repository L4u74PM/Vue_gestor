<script setup>
import { computed, ref } from 'vue'
import TaskForm from './TaskForm.vue'
import TaskList from './TaskList.vue'

const tasks = ref([
  {
    id: 1,
    titulo: 'Aprender Vue.js',
    dataCreacio: '2024-06-01',
    completada: false,
  },
  {
    id: 2,
    titulo: 'Practicar con un proyecto',
    dataCreacio: '2024-06-02',
    completada: false,
  },
  {
    id: 3,
    titulo: 'Revisar la documentación',
    dataCreacio: '2024-06-03',
    completada: true,
  },
])

const mostrarPendientes = ref(false)

const taskFiltradas = computed(() => {
  if (mostrarPendientes.value) {
    return tasks.value.filter((task) => !task.completada)
  }

  return tasks.value
})

const totalTareas = computed(() => tasks.value.length)
const totalPendientes = computed(() => tasks.value.filter((task) => !task.completada).length)

const agregarTarea = (nuevaTarea) => {
  tasks.value.push({
    id: Date.now(),
    ...nuevaTarea,
  })
}

const changeStatus = (task) => {
  const tarea = tasks.value.find((item) => item.id === task.id)

  if (tarea) {
    tarea.completada = !tarea.completada
  }
}

const eliminarTarea = (task) => {
  tasks.value = tasks.value.filter((t) => t.id !== task.id)
}
</script>

<template>
  <div>
    <h1>Task App</h1>
    <TaskForm @add-task="agregarTarea" />

    <div>
      <input type="checkbox" id="pendientes" v-model="mostrarPendientes" />
      <label for="pendientes">Mostrar solo pendientes</label>
    </div>

    <TaskList
      :tasks="taskFiltradas"
      @toggle-status="changeStatus"
      @delete-task="eliminarTarea"
    />

    <p>Totales: {{ totalTareas }}, Pendientes: {{ totalPendientes }}</p>
  </div>
</template>