<template>
  <todo-app></todo-app>
  <router-view />
</template>

<script>
import TodoApp from "./components/TodoApp.vue";
export default {
  data() {
    return {};
  },
  components: { TodoApp },
};
</script>

<style scoped></style>
