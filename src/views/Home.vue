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
    async fetchTodos() {
      try {
        const { data } = await this.axios.get(
          "https://shielded-chamber-71167.herokuapp.com/todos"
        );

        this.todos = data;
      } catch (error) {
        console.log(error);
      }
    }
  },
  async mounted() {
    await this.fetchTodos();
  }
};
</script>
