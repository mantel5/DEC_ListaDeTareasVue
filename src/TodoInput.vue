<script setup lang="ts">
import { ref } from 'vue'

const nuevaTarea = ref('')
const emit = defineEmits(['add-tarea'])

function enviarTarea() {
  if (nuevaTarea.value.trim() === '') return // Evita enviar vacíos
  
  emit('add-tarea', nuevaTarea.value)
  nuevaTarea.value = '' // Limpia el input
}
</script>

<template>
  <div class="input-container">
    <input 
      v-model="nuevaTarea" 
      type="text" 
      placeholder="Escribe una tarea..." 
      @keyup.enter="enviarTarea"
    />
    <button @click="enviarTarea">+</button>
  </div>
</template>

<style scoped>
.input-container {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

input {
  flex-grow: 1;
  padding: 5px;
}
</style>