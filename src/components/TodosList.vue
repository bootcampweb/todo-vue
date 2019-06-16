<template>
  <div class="todos-list">
    <v-list>
      <template v-for="(todo, index) in todos">
        <v-list-tile @click="onTodoClick(todo)" :key="todo.title">
          <v-list-tile-content>
            <v-list-tile-title>
              {{ todo.title }}
            </v-list-tile-title>
          </v-list-tile-content>

          <v-list-tile-action>
            <v-btn icon ripple @click.stop="onDeleteBtnClick(index, todo)">
              <v-icon>delete</v-icon>
            </v-btn>
          </v-list-tile-action>
        </v-list-tile> 

        <v-divider v-if="showDivider(index)" :key="todo.id"></v-divider>
      </template>
    </v-list>

    <v-dialog v-model="dialog" max-width="300" @keydown.esc="cancel">
      <v-card>
        <v-toolbar dense flat>
          <v-toolbar-title>Remover Todo?</v-toolbar-title>
        </v-toolbar>
        <v-card-text>Você deseja realmente remover este todo?</v-card-text>
        <v-card-actions class="pt-0">
          <v-spacer></v-spacer>
          <v-btn color="grey" flat="flat" @click.native="cancel">Cancelar</v-btn>
          <v-btn color="primary darken-1" flat="flat" @click.native="agree">Remover</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import { Promise } from "q";
export default {
  props: {
    todos: Array
  },

  data() {
    return {
      dialog: false,
      resolve: null,
      reject: null
    };
  },

  methods: {
    onTodoClick(todo) {
      this.$emit("clicked", todo.id);
    },

    showDivider(index) {
      return index + 1 < this.todos.length;
    },

    onDeleteBtnClick(index, todo) {
      this.openDialogConfirm().then(remove => {
        if (remove) {
          this.$emit("removeItem", index, todo);
        }
      });
    },

    openDialogConfirm() {
      this.dialog = true;

      return new Promise((resolve, reject) => {
        this.resolve = resolve;
        this.reject = reject;
      });
    },

    agree() {
      this.resolve(true);
      this.dialog = false;
    },
    cancel() {
      this.resolve(false);
      this.dialog = false;
    }
  }
};
</script>
