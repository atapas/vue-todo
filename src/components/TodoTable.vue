<template>
  <div id="todo-table">
    <p v-if="todos.length < 1" class="empty-table">No Todos</p>
    <table v-else>
      <thead>
        <tr>
          <th><h2>TODOs</h2></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todos" :key="todo.id">
          <td v-if="editing === todo.id">
            <input type="text" v-model="todo.name" />
          </td>
          <td v-else>{{ todo.name }}</td>
          <td v-if="editing === todo.id">
            <button @click="editTodo(todo)">Save</button>
            <button class="muted-button" @click="cancelEdit(todo)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(todo)">Edit</button>
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
    data() {
      return {
        editing: null,
      }
    },
    methods: {
      editMode(todo) {
        this.cachedTodo = Object.assign({}, todo)
        this.editing = todo.id
      },
      cancelEdit(todo) {
        Object.assign(todo, this.cachedTodo)
        this.editing = null;
      },
      editTodo(todo) {
        if (todo.name === '') return
        this.$emit('edit:todo', todo.id, todo)
        this.editing = null
      }
    }
  }
</script>

<style scoped>
  button {
    margin: 0 0.5rem 0 0;
  }
</style>