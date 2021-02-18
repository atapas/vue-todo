<template>
  <div id="todo-table">
    <table>
      <thead>
        <tr>
          <th>TODO</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todos" :key="todo.id">
          <td>{{ todo.name }}</td>
          <td>
            <button>Edit</button>
            <button @click="$emit('delete:todo', todo.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'todo-table',
    props: {
        todos: Array,
    },
  }
</script>

<style scoped>
  button {
    margin: 0 0.5rem 0 0;
  }
</style>