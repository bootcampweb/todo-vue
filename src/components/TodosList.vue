<template>
    <v-list>
      <template v-for="(todo, index) in todos">
        <v-list-tile @click="onTodoClick" :key="todo.id">
          <v-list-tile-content>
            <v-list-tile-title>
              {{ todo.title }}
            </v-list-tile-title>
          </v-list-tile-content>  
        </v-list-tile> 

        <v-divider v-if="showDivider(index)" :key="index"></v-divider>
      </template>
    </v-list>
</template>

<script>
export default {
  props: {
    todos: Array
  },

  methods: {
    onTodoClick() {},

    showDivider(index) {
      return index + 1 < this.todos.length;
    }
  }
};
</script>
