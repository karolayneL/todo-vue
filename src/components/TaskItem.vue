<script setup>
import { computed } from 'vue';

const props = defineProps({
  task: {
    type: Object,
    required: true,
    validator: (value) => ['id', 'text', 'done'].every(key => key in value)
  }
});

const emit = defineEmits(['remove']);

const removeTask = () => {
  emit('remove', props.task.id);
};

const taskClasses = computed(() => [
  'task-item',
  { 'task-done': props.task.done }
]);
</script>

<template>
  <div :class="taskClasses">

    <input type="checkbox" v-model="task.done" class="task-checkbox" />
    
    <span class="task-text">{{ task.text }}</span>
    
    <button @click="removeTask" class="remove-btn">
      Remover
    </button>
  </div>
</template>

<style scoped>
.task-item {
  display: flex;
  align-items: center;
  padding: 12px 15px;
  margin-bottom: 8px;
  border-radius: 6px;
  background-color: #E6CCE6;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  transition: all 0.2s ease-in-out;
}

.task-done {
  background-color: #A46BC2; 
  color: #888;
  border-left: 5px solid #5B2C6F;
}

.task-checkbox {
  margin-right: 15px;
  min-width: 18px;
  min-height: 18px;
}

.task-text {
  flex-grow: 1;
  font-size: 1.1em;
}

.task-done .task-text {
  text-decoration: line-through;
  color: #a0aec0;
}

.remove-btn {
  background-color: #C8A2C8; 
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 20px;
  transition: background-color 0.2s;
}

.remove-btn:hover {
  background-color: #5B2C6F;
}
</style>