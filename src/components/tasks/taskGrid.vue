<script setup>
import TaskItem from './taskItem.vue'

defineProps({
  tasks: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @taskDelete="$emit('taskDelete', task.id)"
        @taskStateChange="$emit('taskStateChange', task.id)"
      />
    </template>

    <p class="no-task" v-else>Your life is up to date :)</p>
  </div>
</template>

<style scoped>
  .task-grid {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    flex: 1;
    gap: 0.625rem;

    width: 100%;
  }

  .task-grid .no-task {
    font-size: 1.4rem;
  }
</style>
