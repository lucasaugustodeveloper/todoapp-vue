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
    <span class="close" @click="$emit('taskDelete', task)">x</span>
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
  position: relative;
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
  border-color: #0a8f08;
  background-color: #4caf50;
  color: #dddddd;
}

.task.done p {
  text-decoration: line-through;
}

.close {
  font-size: 0.725rem;
  font-weight: 700;
  text-align: center;

  display: flex;
  justify-content: center;
  align-items: flex-start;

  width: 1.5rem;
  height: 1.5rem;
  border-radius: 4rem;
  padding-top: 0.15rem;

  position: absolute;
  right: 0.625rem;
  top: 0.625rem;
  
  cursor: pointer;
  user-select: none;
}

.pending .close {
  background-color: #b73229;
}
.done .close {
  background-color: #0a8f08;
}
</style>
