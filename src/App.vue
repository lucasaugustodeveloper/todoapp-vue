<script setup>
import { ref } from 'vue'

import HelloWorld from './components/HelloWorld.vue'
import TaskGrid from './components/tasks/taskGrid.vue';

const tasks = ref([
  {
    name: 'Task 1',
    pending: false
  },
  {
    name: 'Task 2',
    pending: true
  }
])
</script>

<template>
  <header>
    <div class="wrapper">
      <HelloWorld text="TodoApp Vue" />
    </div>
  </header>

  <main>
    <TaskGrid :tasks="tasks" />
  </main>
</template>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  flex: 1;

  width: 100%;
  padding: 1rem;
}
</style>
