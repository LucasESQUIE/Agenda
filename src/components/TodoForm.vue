<template>
  <div>
    <form @submit="addTodo">
      <div class="form-group text-center">
        <input type="text" class="form-control" v-model="title" name="title" />
      </div>
      <div class="text-center">
        <button type="submit" class="btn btn-primary button">Add</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "todo-form",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      if (this.title != "") {
        const todo = {
          title: this.title,
          completed: false
        };
        this.$emit("add-todo", todo);
        this.title = "";
      } else {
        this.$notify({
          group: "errors",
          type: "error",
          duration: 1500,
          text: "Title shouldn't be empty !"
        });
      }
    }
  }
};
</script>

<style>
.button {
  width: 20%;
}
</style>