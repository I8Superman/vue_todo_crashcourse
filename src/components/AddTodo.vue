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
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
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