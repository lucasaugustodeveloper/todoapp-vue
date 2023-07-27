<script setup>
import { defineProps, computed } from 'vue'

const props = defineProps({
  task: {
    type: Object,
    required: true
  },
})

const stateClass = computed(() => {
  return {
    pending: props.task.pending,
    done: !props.task.pending
  }
})
</script>

<template>
  <div class="task" :class="stateClass">
    <p>{{ task.name }}</p>
  </div>
</template>

<style scoped>
.task {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;

  max-width: 350px;
  width: 100%;

  padding: 0.625rem;

  border-left-style: solid;
  border-left-width: 0.625rem;
  border-radius: 0.5rem;

  cursor: pointer;
  user-select: none;
}

.task p {
  font-size: 2rem;
  font-weight: 400;
  text-align: center;
}

.task.pending {
  border-color: #b73229;
  background-color: #f44336;
}

.task.done {
  text-decoration: line-through;

  border-color: #0a8f08;
  background-color: #4caf50;
  color: #dddddd;
}
</style>
