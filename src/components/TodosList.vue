<template>
    <div>
    <v-list>
      <template v-for="(todo, index) in todos">
        <v-list-tile @click="onTodoClick(todo)" :key="todo.title">
          <v-list-tile-content>
            <v-list-tile-title>
              {{ todo.title }}
            </v-list-tile-title>
          </v-list-tile-content>

          <v-list-tile-action>
            <v-btn icon ripple @click.stop="onDeleteBtnClick(todo)">
              <v-icon>delete</v-icon>
            </v-btn>
          </v-list-tile-action>
        </v-list-tile> 

        <v-divider v-if="showDivider(index)" :key="todo.id"></v-divider>
      </template>
    </v-list>

    <v-dialog
                v-model="dialog"
                width="500"
              >

                <v-card>
                  <v-card-title
                    class="headline grey lighten-2"
                    primary-title
                  >
                    Remover Todo?
                  </v-card-title>

                  <v-card-text>
                    <p>Você deseja realmente remover este todo?</p>
                  </v-card-text>

                  <v-divider></v-divider>

                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                      color="default"
                      flat
                      @click="dialog = false"
                    >
                      Cancelar
                    </v-btn>
                    <v-btn
                      color="primary"
                      flat
                      @click="dialog = false"
                    >
                      Remover
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
    </div>
</template>

<script>
export default {
  props: {
    todos: Array
  },

  methods: {
    onTodoClick(todo) {
      this.$emit("clicked", todo.id);
    },

    showDivider(index) {
      return index + 1 < this.todos.length;
    },

    onDeleteBtnClick(todo) {
      //this.$emit("remove", todo);
      this.dialog = true;
    }
  }
};
</script>
