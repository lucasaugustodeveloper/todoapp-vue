<script setup>
defineProps({
  text: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="greetings">
    <h1>{{ text }}</h1>
  </div>
</template>

<style scoped>
  h1 {
    font-size: 3rem;
    font-weight: 300;
  }
</style>
