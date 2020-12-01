<template>
  <div class="container-fluid">
    <div class="container">
      <todo-app />
    </div>
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue'

export default {
  components: { TodoApp },
  name: 'App',
}
</script>

<style>
</style>
