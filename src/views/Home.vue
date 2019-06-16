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
            top
            right
            dark
            color="pink"
            @click="goToAddTodo">
              <v-icon>add</v-icon>
            </v-btn>
          <TodosList :todos="todos" @clicked="onTodoClicked" @removeItem="onTodoRemove"></TodosList>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
// @ is an alias to /src
import TodosList from "@/components/TodosList.vue";
import { log } from "util";

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
        const url = `${process.env.VUE_APP_API_BASE_URL}/todos`;
        const { data } = await this.axios.get(url);

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

    async onTodoRemove(index, todo) {
      try {
        const url = `${process.env.VUE_APP_API_BASE_URL}/todos/${todo.id}`;
        await this.axios.delete(url);

        this.todos.splice(index, 1);
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
