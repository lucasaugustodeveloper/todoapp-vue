<script setup>
import { ref, computed } from 'vue'
import { uid } from 'uid/secure'

import HelloWorld from './components/HelloWorld.vue'
import TaskGrid from './components/tasks/taskGrid.vue';
import TaskNew from './components/tasks/newTask.vue';
import TaskProgress from './components/tasks/taskProgress.vue';

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
const toggleStateTask = id => {
    const newTasks = tasks.value.map(task => {
    if (task.id === id) {
      return {
      ...task,
        pending: !task.pending
      }
    }

    return task
  })

  tasks.value = newTasks
}
const progress = computed(() => {
  const total = tasks.value.length
  const done = tasks.value.filter(t => !t.pending).length

  return Math.round(done / total * 100) || 0
})
</script>

<template>
  <header>
    <div class="wrapper">
      <HelloWorld text="TodoApp Vue" />
    </div>

    <TaskProgress :progress="progress" />

    <TaskNew @taskAdd="addTask" />
  </header>

  <main>
    <TaskGrid
      :tasks="tasks"
      @taskDelete="deleteTask"
      @taskStateChange="toggleStateTask"
    />
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
