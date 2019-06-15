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
      todos: []
    };
  },
  methods: {
    fetchTodos() {
      this.axios
        .get("https://shielded-chamber-71167.herokuapp.com/todos")
        .then(res => {
          const { data } = res;
          this.todos = data;
        })
        .catch(err => console.log(err));
    }
  },
  mounted() {
    this.fetchTodos();
  }
};
</script>
