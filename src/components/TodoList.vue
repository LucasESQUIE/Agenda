<template>
  <table class="table mt-5 table-borderless">
    <tbody v-bind:key="todo.id" v-for="todo in todos">
      <Todo v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo._id)" />
    </tbody>
  </table>
</template>

<script>
import Todo from "./Todo";

export default {
  name: "TodoList",
  components: {
    Todo
  },
  props: ["todos"]
};
</script>

<style>
table {
  width: 100%;
}
</style>