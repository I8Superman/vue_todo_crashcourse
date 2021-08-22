<template>
  <div id="app">
    <!-- <Header /> Removed as we use routing instead-->
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
// import Header from "../components/layout/Header";  Removed. Replaced by routing.
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";

export default {
  name: "Home",
  components: {
    // Header,  Removed as routing is implemented
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      fetch("http://localhost:5000/todos/" + id, {
        method: "delete",
        headers: {
          "Content-Type": "application/json; charset=utf-8",
          "cache-control": "no-cache",
        },
      })
        .then((res) => res.json())
        .then((deleteData) => console.log(deleteData));

      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodo(newTodo) {
      //const { title, completed } = newTodo;

      fetch("http://localhost:5000/todos", {
        method: "post",
        body: JSON.stringify(newTodo),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((res) => res.json())
        .then((postData) => {
          //console.log(postData);
          this.todos = [...this.todos, postData]; // Why do I need to add it to my arr too? Shouldn't it update automatically based on the db?
        });
    },
  },
  created() {
    fetch("http://localhost:5000/todos") // Fetching from fake, local jso db - nice!
      .then((res) => res.json())
      .then((data) => {
        this.todos = data;
        // console.log(this.todos);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
  transition: all 0.5s;
}

.btn:hover {
  background: #888;
}
</style>

