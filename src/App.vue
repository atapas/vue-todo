<template>
  <div id="app" class="small-container">
    <send-feedback class="sendFeedback"/>
    <h1>Bugfender TODO</h1>
    <todo-form @add:todo="addTodo" />
    <todo-table 
      :todos="todos" 
      @delete:todo="deleteTodo" 
      @edit:todo="editTodo" />
    <br />
    
  </div>
</template>

<script>
import TodoTable from "@/components/TodoTable.vue";
import TodoForm from "@/components/TodoForm.vue";
import SendFeedback from "@/components/SendFeedback.vue";

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
    SendFeedback
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
      const id = generate();
      const newTodo = { ...todo, id };

      this.todos = [...this.todos, newTodo];
      Bugfender.log(`Added a TODO with id ${id}, and name ${todo.name}`);
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(
        todo => todo.id !== id
      )
      Bugfender.log(`Deleted a TODO with id ${id}`);
    },
    editTodo(id, updatedTodo) {
      this.todos = this.todos.map(todo =>
        todo.id === id ? updatedTodo : todo
      )
      Bugfender.log(`Updated a TODO with id ${updatedTodo.id}, and name ${updatedTodo.name}`);
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
  margin-top: 15px;
}

button {
  background: #ff5060;
  border: 1px solid #ff5060;
  color: #FFFFFF;
  padding: 5px;
  border-radius: 4px;
  cursor: pointer;
}

.sendFeedback {
  position: absolute;
  top:10px;
  right: 30px;
}

.small-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 0.9em;
  font-family: sans-serif;
  min-width: 400px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
  width: 100%;
}

table thead tr {
  text-align: left;
}

table th {
  padding: 12px 25px;
}

table td {
  padding: 12px 15px;
}

table tbody tr {
  border-bottom: 1px solid #dddddd;
}

table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}

table tbody tr:last-of-type {
  border-bottom: 2px solid #ff5060;
}

table tbody tr.active-row {
  font-weight: bold;
  color: #ff5060;
}

label {
    font-weight: 600;
    max-width: 100%;
    display: block;
    margin: 1rem 0 0.5rem;
}

input[type=text] {
  display: block;
  border: 1px solid #dedede;
  border-radius: 4px;
  padding: 0.75rem;
  outline: none;
  background: transparent;
  margin-bottom: 0.5rem;
  font-size: 1rem;
  width: 100%;
  max-width: 100%;
  line-height: 1;
}

</style>
