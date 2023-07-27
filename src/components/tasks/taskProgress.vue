<script setup>
defineProps({
  progress: {
    type: Number,
    required: true,
  }
})
</script>

<template>
  <div class="tasks-progress">
    <span class="progress-value">{{ progress }}%</span>
    <div class="progress-bar" :style="{width: `${progress}%`}" />
  </div>
</template>

<style scoped>
  .tasks-progress {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    position: relative;
    width: 50%;
    border-style: solid;
    border-width: 0.1rem;
    border-radius: 4rem;
    overflow: hidden;

    border-color: #ffffff;
    color: #ffffff;
  }

  .progress-value {
    font-size: 1.2rem;
    font-weight: 700;
    z-index: 1;
  }

  .progress-bar {
    align-self: flex-start;

    border-radius: 4rem;
    height: 100%;

    position: absolute;
    left: 0;
    top: 0;

    background-color: #4caf50;
  }
</style>
