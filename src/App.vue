<template>
  <div>
    <form @submit.prevent="addTask">
      <h2 contenteditable="true" @input="updateTitle($event)">{{ titulo }}</h2>
      <input v-model.trim="nuevaTarea" placeholder="Agrega una tarea" required @keyup.enter="addTask">
      <button type="submit">Agregar Tarea</button>
    </form>

    <ul>
      <li v-for="task in tareas" :key="task.id">
        <input v-model="task.name" @change="editTask(task.id)">
        <button @click="deleteTask(task.id)">Borrar tarea</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';

let nuevaTarea = ref('');
let tareas = reactive([]);
let titulo = ref('Lista de tareas');

const addTask = () => {
  const id = tareas.length + 1;
  tareas.push({ id, name: nuevaTarea.value });
  nuevaTarea.value = '';
};
const deleteTask = (id) => {
  const index = tareas.findIndex(task => task.id === id);
  if (index !== -1) {
    tareas.splice(index, 1);
  }
};
const editTask = (id) => {
  const task = tareas.find(task => task.id === id);
  nuevatarea.value = task.name;
  nuevaTarea.value = '';
};
const updateTitle = (event) => {
  title.value = event.target.innerText;
};
</script>

<style scoped>
form {
  padding: 15px 15px;
  margin: 0 5px;
}

form h2 {
  padding: 5px 5px;
  color: black;
  font-weight: bold;
  font-size: 32px;
  margin-bottom: 10px;
  width: 30%;
}
</style>