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
                <div class="display-1 pl-5">Adicionar Todo</div>
              </v-card-title>
            </v-layout>
          </v-img>

          <TodoForm @submited="addTodo"></TodoForm>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import TodoForm from "@/components/TodoForm.vue";
export default {
  components: {
    TodoForm
  },
  methods: {
    async addTodo(todo) {
      try {
        const url = `${process.env.VUE_APP_API_BASE_URL}/todos`;
        const { data } = await this.axios.post(url, todo);

        this.$router.push({ path: "/" });
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>