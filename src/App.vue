<script setup>
import { ref } from 'vue';
import TaskList from './components/TaskList.vue';

const newTaskText = ref('');

const tasks = ref([
  { id: 1, text: 'Desenvolver componentes', done: true },
  { id: 2, text: 'Implementar a função de adicionar', done: false },
  { id: 3, text: 'Estilizar as tarefas', done: false }
]);

const addTask = () => {
  if (newTaskText.value.trim() === '') {
    alert('A tarefa não pode ser vazia!');
    return;
  }

  const newId = tasks.value.length > 0
    ? Math.max(...tasks.value.map(t => t.id)) + 1
    : 1;

  tasks.value.push({
    id: newId,
    text: newTaskText.value.trim(),
    done: false
  });

  newTaskText.value = '';
};

const removeTask = (taskId) => {
  tasks.value = tasks.value.filter(task => task.id !== taskId);
};
</script>

<template>
  <div id="todo-app-wrapper">
    <header class="app-header">
      <h1>Lista de Tarefas (To-Do List)</h1>
      <p>Desenvolvido com Vue 3, Componentização e Binding de Dados.</p>
    </header>

    <div class="task-form-section">
      <input
        type="text"
        v-model="newTaskText"
        placeholder="Adicione uma nova tarefa (Ex: Comprar pão)"
        @keyup.enter="addTask"
        class="task-input"
      />
      <button @click="addTask" class="add-button">
        Adicionar Tarefa
      </button>
    </div>

    <TaskList :tasks="tasks" @remove-task="removeTask" />
  </div>
</template>

<style scoped>
#todo-app-wrapper {
  max-width: 700px;
  margin: 50px auto;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  background-color: #E056FD;
  font-family: 'Arial', sans-serif;
}

.app-header {
  text-align: center;
  margin-bottom: 30px;
}

.app-header h1 {
  color: #4B4453;
  font-size: 2.2em;
  border-bottom: 2px solid #E7CBA9;
  padding-bottom: 10px;
  display: inline-block;
}

.task-form-section {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.task-input {
  flex-grow: 1;
  padding: 12px;
  border: 2px solid #5B2C6F;
  border-radius: 6px;
  font-size: 1em;
  transition: border-color 0.2s;
}

.task-input:focus {
  border-color: #5B2C6F;
  outline: none;
}

.add-button {
  padding: 12px 20px;
  background-color: #C8A2C8; 
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
  transition: background-color 0.2s, transform 0.1s;
}

.add-button:hover {
  background-color: #5B2C6F;
}

.add-button:active {
  transform: scale(0.98);
}
</style>