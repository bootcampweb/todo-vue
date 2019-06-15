<template>
  <v-container>
    <v-layout row>
      <v-flex xs12 sm6 offset-sm3>
        <v-card>
          <v-img
            src="https://i.stack.imgur.com/3jASk.jpg"
            height="300px">
            <v-layout column fill-height>
              <v-spacer></v-spacer>
              <v-card-title class="white--text pl-5">
                <div class="display-1 pl-5">Meus Todo's</div>
              </v-card-title>
            </v-layout>
          </v-img>
          <v-btn fab
            absolute
            center
            right
            dark
            color="pink"
            @click="goToAddTodo">
              <v-icon>add</v-icon>
            </v-btn>
          <TodosList :todos="todos" @clicked="onTodoClicked" @remove="onTodoRemove"></TodosList>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
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
      todos: [],
      dialog: false
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
    },
    goToAddTodo() {
      this.$router.push({ path: "add-todo" });
    },
    onTodoClicked(id) {
      this.$router.push({ path: `edit-todo/${id}` });
    },
    onTodoRemove(todo) {
      console.log(todo);
    }
  },
  async mounted() {
    await this.fetchTodos();
  }
};
</script>
