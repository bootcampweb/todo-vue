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
                <div class="display-1 pl-5">Editar Todo</div>
              </v-card-title>
            </v-layout>
          </v-img>

          <TodoForm :selectedTodo="todo" @submited="editTodo"></TodoForm>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import TodoForm from "@/components/TodoForm.vue";
export default {
  props: ["id"],
  components: {
    TodoForm
  },

  data() {
    return {
      todo: {}
    };
  },

  async beforeMount() {
    try {
      const url = `${process.env.VUE_APP_API_BASE_URL}/todos/${this.id}`;
      const { data } = await this.axios.get(url);

      this.todo = data;
    } catch (error) {
      console.log(error);
    }
  },

  methods: {
    async editTodo(todo) {
      try {
        const url = `${process.env.VUE_APP_API_BASE_URL}/todos/${todo.id}`;
        const { data } = await this.axios.put(url, todo);

        this.$router.push({ path: "/" });
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>