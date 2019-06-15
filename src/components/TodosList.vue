<template>
    <v-list>
      <template v-for="(todo, index) in todos">
        <v-list-tile @click="onTodoClick(todo)" :key="todo.title">
          <v-list-tile-content>
            <v-list-tile-title>
              {{ todo.title }}
            </v-list-tile-title>
          </v-list-tile-content>  
        </v-list-tile> 

        <v-divider v-if="showDivider(index)" :key="todo.id"></v-divider>
      </template>
    </v-list>
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
    }
  }
};
</script>
