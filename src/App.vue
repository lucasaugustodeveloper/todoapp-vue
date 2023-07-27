<script setup>
import { ref } from 'vue'
import { uid } from 'uid/secure'

import HelloWorld from './components/HelloWorld.vue'
import TaskGrid from './components/tasks/taskGrid.vue';
import TaskNew from './components/tasks/newTask.vue';

const tasks = ref([
  {
    id: uid(),
    name: 'Task 1',
    pending: false
  },
  {
    id: uid(),
    name: 'Task 2',
    pending: true
  }
])

const addTask = task => {
  const sameName = t => t.name === task.name
  const reallyNew = tasks.value.filter(sameName).length === 0

  reallyNew && tasks.value.push({
    id: uid(),
    name: task.name,
    pending: true
  })
}
const deleteTask = id => {
  const newTasks = tasks.value.filter(task => task.id !== id)

  tasks.value = newTasks
}
</script>

<template>
  <header>
    <div class="wrapper">
      <HelloWorld text="TodoApp Vue" />
    </div>

    <TaskNew @taskAdd="addTask" />
  </header>

  <main>

    <TaskGrid :tasks="tasks" @taskDelete="deleteTask" />
  </main>
</template>

<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  width: 100%;
}
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
