<script setup>
import { ref, computed, onMounted, watchEffect } from 'vue'
import { uid } from 'uid/secure'

import HelloWorld from './components/HelloWorld.vue'
import TaskGrid from './components/tasks/taskGrid.vue';
import TaskNew from './components/tasks/newTask.vue';
import TaskProgress from './components/tasks/taskProgress.vue';

const tasks = ref([])

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

watchEffect(() => {
  if (tasks.value.length) {
    localStorage.setItem('tasks', JSON.stringify(tasks.value))
  }
})

onMounted(() => {
  const localTasks = JSON.parse(localStorage.getItem('tasks'))

  if (Array.isArray(localTasks)) {
    return tasks.value = localTasks
  }

  tasks.value = []
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
