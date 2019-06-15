<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Bootcamp Todos</h1>
    <TodosList :todos="todos"></TodosList>
  </div>
</template>

<script>
// @ is an alias to /src
import TodosList from "@/components/TodosList.vue";

export default {
  name: "home",
  components: {
    TodosList
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Lista 1",
          created_by: "2"
        },
        {
          id: 2,
          title: "Lista 2",
          created_by: "2"
        },
        {
          id: 3,
          title: "Lista 3",
          created_by: "2"
        }
      ]
    };
  }
};
</script>
