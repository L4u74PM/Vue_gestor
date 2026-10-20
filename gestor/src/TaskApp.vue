
<template>
  <h1>Task App</h1>
  <p>
   Una simple aplicación de tareas para practicar
  </p>
  <div>
    <label for="task">Nueva tarea:</label>
    <input v-model="nuevaTarea" type="text" id="task" placeholder="Nueva tarea" />
    <button @click="agregarTarea">Agregar</button>
  </div>
  <div>
    <h2>Lista de tareas</h2>
    <ul>
      <li  v-for="task in tasks" :key="task.id">
        <span v-if="!task.completada">{{ task.titulo }} - {{ task.dataCreacio }} - <button @click="changeStatus(task)">completar</button><button @click="eliminarTarea(task)">Eliminar</button></span>
        <span v-else style="text-decoration: line-through;">{{ task.titulo }} - {{ task.dataCreacio }} - <button @click="changeStatus(task)">descompletar</button> <button @click="eliminarTarea(task)">Eliminar</button></span>
      </li>
      
    </ul>
  </div>
</template>
<script setup>
import { ref } from 'vue'

const tasks = ref([
    {
        id: 1,
        titulo: 'Aprender Vue.js',
        dataCreacio: '2024-06-01',
        completada: false
    },
    {
        id: 2,
        titulo: 'Practicar con un proyecto',
        dataCreacio: '2024-06-02',
        completada: false
    },
    {
        id: 3,
        titulo: 'Revisar la documentación',
        dataCreacio: '2024-06-03',
        completada: true
    }
])

const nuevaTarea = ref('')

const agregarTarea = () => {
    if (nuevaTarea.value.trim() !== '') {
        tasks.value.push({
            id: tasks.value.length + 1,
            titulo: nuevaTarea.value,
            dataCreacio: new Date().toISOString().split('T')[0],
            completada: false
        })
        nuevaTarea.value = ''
    }
}

const changeStatus = (task) => {
    task.completada = !task.completada
}
const eliminarTarea = (task) => {
    tasks.value = tasks.value.filter(t => t.id !== task.id)
}
</script>