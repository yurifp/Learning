<script setup lang="ts">
import { ref } from 'vue';

interface Task {
  id: number;
  text: string;
}

const newTask = ref('');
const tasks = ref<Task[]>([]);
let nextId = 0;

function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({
      id: nextId++,
      text: newTask.value.trim()
    });
    newTask.value = '';
  }
}

function removeTask(id: number) {
  const index = tasks.value.findIndex(task => task.id === id);
  if (index > -1) {
    tasks.value.splice(index, 1);
  }
}
</script>

<template>
  <div class="todo-container">
    <h1>Minha ToDo List</h1>

    <div class="input-section">
      <input 
        v-model="newTask" 
        @keyup.enter="addTask" 
        placeholder="Digite uma nova tarefa" 
      />
      <button @click="addTask">Adicionar</button>
    </div>

    <ul>
      <!-- ✅ Usando ID único como key -->
      <li v-for="task in tasks" :key="task.id">
        {{ task.text }}
        <button @click="removeTask(task.id)">Remover</button>
      </li>
    </ul>
  </div>
</template>