<template>
  <div class="container text-center">
    <h1 class="display-3">Todo App</h1>
    <hr />
    <notifications group="errors" position="center" />
    <div class="row">
      <div class="text-center topSpacing col-lg-12">
        <TodoForm v-on:add-todo="addTodo" />
      </div>
    </div>
    <div class="row">
      <div class="col-lg-12">
        <TodoList v-bind:todos="todos" v-on:del-todo="deleteTodo" />
      </div>
    </div>
  </div>
</template>

<script>
const API_URL = "http://localhost:5000/api/todos";

import Vue from "vue";
import Notifications from "vue-notification";

Vue.use(Notifications);

import TodoList from "./components/TodoList";
import TodoForm from "./components/TodoForm";

export default {
  name: "app",
  components: {
    TodoList,
    TodoForm
  },
  data() {
    return {
      todos: []
    };
  },

  methods: {
    addTodo(todo) {
      fetch(API_URL, {
        method: "POST",
        body: JSON.stringify(todo),
        headers: {
          "content-type": "application/json"
        }
      }).then(() => {
        fetch(API_URL)
          .then(res => res.json())
          .then(todos => (this.todos = todos));
      });
    },
    deleteTodo(id) {
      fetch(API_URL + "/" + id, {
        method: "DELETE"
      });

      fetch(API_URL)
        .then(res => res.json())
        .then(todos => (this.todos = todos.filter(todo => todo._id != id)));
    }
  },

  created() {
    fetch(API_URL)
      .then(res => res.json())
      .then(todos => (this.todos = todos));
  }
};
</script>

<style>
.topSpacing {
  margin-top: 7%;
}

div.row {
  width: 100%;
}
</style>
