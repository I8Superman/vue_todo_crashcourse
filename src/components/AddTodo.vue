<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="Add new todo..."
      />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
// import { v4 as uuidv4 } from "uuid"; - no need for it after using json placeholder fake server

export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo(event) {
      event.preventDefault();
      const newTodo = {
        // id: uuidv4(),
        // id: nextId,
        title: this.title,
        completed: false,
      };
      this.$emit("add-todo", newTodo); // Sending the whole todo object to the parent component (App.vue)
      this.title = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}

input[type="text"] {
  flex: 8;
  padding: 5px;
}

input[type="submit"] {
  flex: 2;
}
</style>