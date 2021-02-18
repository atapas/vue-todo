<template>
  <div id="todo-form">
    <form @submit.prevent="handleSubmit">
      <label>Add a TODO</label>
      <input v-model="todo.name" type="text" />
      <button>Add</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'todo-form',
    data() {
      return {
        todo: {
          name: ''
        },
      }
    },
    methods: {
        handleSubmit() {
            this.$emit('add:todo', this.todo)
        },
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>