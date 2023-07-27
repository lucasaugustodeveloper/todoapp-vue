<script>
export default {
  data() {
    return {
      name: '',
    }
  },
  methods: {
    add() {
      this.$emit('taskAdd', { name: this.name })
      this.name = ''
    },
  }
}
</script>

<template>
  <div class="task-new">
    <input
      class="form-element element"
      placeholder="Enter your task"
      type="text"
      v-model="name"
      @keydown.enter="add"
    />
    <button class="btn element" type="button" @click="add">+</button>
  </div>
</template>

<style scoped>
.task-new {
  display: flex;
  margin: 2.5rem 0;
  width: 50%;
}

.form-element {
  font-size: 2rem;
  outline: none;

  border: 0.1rem solid #ffffff;
  padding: 0.5rem;

  width: 100%;
  border-top-left-radius: 0.625rem;
  border-bottom-left-radius: 0.625rem;

  background-color: rgba(255, 255, 255, 0.2);
  color: #ffffff;
}
.btn {
  font-size: 2.5rem;
  font-weight: 700;

  padding: 0.5rem;
  width: 3rem;
  border: 0.1rem solid #ffffff;
  border-left: none;
  border-top-right-radius: 0.625rem;
  border-bottom-right-radius: 0.625rem;

  background-color: #2196f3;
  color: #ffffff;
}
</style>
