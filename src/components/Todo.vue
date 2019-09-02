<template>
  <tr class="mt-3 todo" v-bind:class="{'is-complete': todo.completed}">
    <td>
      <input type="checkbox" v-on:change="todoComplete" />
    </td>
    <td class="title">{{todo.title}}</td>
    <td>
      <input type="button" value="Delete" @click="deleteTodo" class="btn btn-danger" />
    </td>
  </tr>
</template>

<script>
export default {
  name: "todo",
  props: ["todo"],
  methods: {
    todoComplete() {
      this.todo.completed = !this.todo.completed;
    },
    deleteTodo() {
      this.$emit("del-todo", this.todo._id);
    }
  }
};
</script>

<style scoped>
.is-complete {
  background-color: gray;
}
.todo {
  width: 100%;
}
.title {
  font-size: 18px;
  font-family: Arial, Helvetica, sans-serif;
}
</style>