<script setup lang="ts">
// Definimos la estructura exacta de los objetos
defineProps<{
  tareas: { id: number, texto: string, hecha: boolean }[]
}>()

// Definimos los dos eventos que puede emitir este componente
const emit = defineEmits(['borrar-tarea', 'cambiar-estado'])
</script>

<template>
  <ul>
    <li v-for="tarea in tareas" :key="tarea.id">
      
      <input 
        type="checkbox" 
        :checked="tarea.hecha" 
        @change="emit('cambiar-estado', tarea.id)"
      >
      
      <span :class="{ tachado: tarea.hecha }">
        {{ tarea.texto }}
      </span>
      
      <button @click="emit('borrar-tarea', tarea.id)">🗑️</button>
    </li>
  </ul>
</template>

<style scoped>
ul {
  padding: 0;
  list-style: none;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center; /* Centra verticalmente */
  margin-bottom: 10px;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
}

.tachado {
  text-decoration: line-through;
  color: gray;
}
</style>