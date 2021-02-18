<template>
  <div id="app" class="small-container">
    <h1>Bugfender TODO</h1>
    <todo-form @add:todo="addTodo" />
    <todo-table :todos="todos" @delete:todo="deleteTodo" />
  </div>
</template>

<script>
import TodoTable from "@/components/TodoTable.vue";
import TodoForm from "@/components/TodoForm.vue";

import { Bugfender } from '@bugfender/sdk';
import { generate } from 'shortid';

Bugfender.init({
    appKey: process.env.VUE_APP_BUGFENDER_API_KEY,
    // apiURL: 'https://api.bugfender.com',
    // baseURL: 'https://dashboard.bugfender.com',
    // overrideConsoleMethods: true,
    // printToConsole: true,
    // registerErrorHandler: true,
    // logBrowserEvents: true,
    // logUIEvents: true,
    // version: '',
    // build: '',
});

export default {
  name: "App",
  components: {
    TodoTable,
    TodoForm,
  },
  data() {
    return {
      todos: [
        {
          id: generate(),
          name: "Log a Defect"
        },
        {
          id: generate(),
          name: "Exercise"
        },
        {
          id: generate(),
          name: "Buy Milk"
        },
      ],
    };
  },
  methods: {
    addTodo(todo) {
      Bugfender.log('From the vue app', todo);
     
      const id = generate();
      const newTodo = { ...todo, id };

      this.todos = [...this.todos, newTodo];
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(
        todo => todo.id !== id
      )
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  background: #005994;
  border: 1px solid #005994;
  color: #FFFFFF;
}

.small-container {
  max-width: 680px;
}
</style>
