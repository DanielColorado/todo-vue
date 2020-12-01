<template>
  <h1 class="d-flex justify-content-between align-items-center">
    TODO
    <span
      @click="changeTheme"
      class="d-flex justify-content-center align-items-center"
    >
      <img :src="imgTheme" alt="" />
    </span>
  </h1>
  <todo-form />
  <todo-list />
</template>

<script>
import { provide, ref, watchEffect } from "vue";
import TodoForm from "./TodoForm.vue";
import TodoList from "./TodoList.vue";
export default {
  components: { TodoForm, TodoList },
  setup() {
    const todos = ref([]);
    const currentTheme = ref("");
    const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)");
    const imgTheme = ref("../img/icon-moon.svg");

    provide("todos", todos);

    if (localStorage.getItem("todos")) {
      todos.value = JSON.parse(localStorage.getItem("todos"));
    }

    if (localStorage.getItem("theme")) {
      currentTheme.value = localStorage.getItem("theme");
    }

    if (currentTheme.value === "dark") {
      document.body.classList.toggle("dark-theme");
      imgTheme.value = "../img/icon-sun.svg";
    } else if (currentTheme.value === "light") {
      document.body.classList.toggle("light-theme");
      imgTheme.value = "../img/icon-moon.svg";
    }

    const changeTheme = () => {
      let theme = "";
      if (prefersDarkScheme.matches) {
        document.body.classList.toggle("light-theme");
        theme = document.body.classList.contains("light-theme")
          ? "light"
          : "dark";
      } else {
        document.body.classList.toggle("dark-theme");
        theme = document.body.classList.contains("dark-theme")
          ? "dark"
          : "light";
      }
      imgTheme.value =
        theme === "light" ? "../img/icon-moon.svg" : "../img/icon-sun.svg";
      localStorage.setItem("theme", theme);
    };

    watchEffect(() => {
      // console.log(todos.value.length)
      // console.log(todos.value)
      localStorage.setItem("todos", JSON.stringify(todos.value));
    });

    return { imgTheme, changeTheme };
  },
};
</script>

<style></style>
