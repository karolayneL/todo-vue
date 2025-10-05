<script setup>
import TaskItem from './TaskItem.vue';

const props = defineProps({
  tasks: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(['remove-task']);

const handleRemove = (taskId) => {
  emit('remove-task', taskId);
};
</script>

<template>
  <div class="task-list-container">
    <h2 v-if="tasks.length > 0">Minhas Tarefas ({{ tasks.length }})</h2>
    <div v-else class="empty-message">A lista está vazia! Adicione uma tarefa acima.</div>

    <div class="list-wrapper">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @remove="handleRemove"
      />
    </div>
  </div>
</template>

<style scoped>
.task-list-container {
  margin-top: 30px;
}
.empty-message {
  padding: 20px;
  text-align: center;
  color: #4B4453;
  background-color: #4B4453;
  border-radius: 8px;
}
.list-wrapper {
  max-height: 50vh;
  overflow-y: auto;
  padding-right: 10px; 
}
</style>