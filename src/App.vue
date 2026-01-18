<script setup lang="ts">
import { ref, computed } from 'vue'
import TodoInput from './TodoInput.vue'
import TodoList from './TodoList.vue'

// 1. ESTADO: Lista de tareas inicial
const listaTareas = ref([
  { id: 1, texto: 'Aprender Vue', hecha: false },
  { id: 2, texto: 'Hacer la compra', hecha: true }
])

// 2. COMPUTED: Cuenta cuántas tareas tienen hecha = true
const tareasHechas = computed(() => {
  return listaTareas.value.filter(tarea => tarea.hecha).length
})

// 3. FUNCIONES
function agregarTarea(textoRecibido: string) {
  const nuevaTarea = {
    id: Date.now(),
    texto: textoRecibido,
    hecha: false
  }
  listaTareas.value.push(nuevaTarea)
}

function eliminarTarea(id: number) {
  listaTareas.value = listaTareas.value.filter(t => t.id !== id)
}

function alternarEstado(id: number) {
  // Busca la tarea por ID y le da la vuelta al valor 'hecha'
  const tarea = listaTareas.value.find(t => t.id === id)
  if (tarea) {
    tarea.hecha = !tarea.hecha
  }
}
</script>

<template>
  <main>
    <h1>Mi To-Do List</h1>
    
    <TodoInput @add-tarea="agregarTarea" />

    <TodoList 
      :tareas="listaTareas" 
      @borrar-tarea="eliminarTarea"
      @cambiar-estado="alternarEstado"
    />

    <div class="contador">
       Total: {{ tareasHechas }} / {{ listaTareas.length }}
    </div>
  </main>
</template>

<style scoped>
main {
  max-width: 500px;
  margin: 0 auto;
  font-family: sans-serif;
}
.contador {
  margin-top: 20px;
  font-weight: bold;
  text-align: right;
  border-top: 2px solid #333;
  padding-top: 10px;
}
</style>