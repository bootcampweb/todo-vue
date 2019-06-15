<template>
    <ul class="todos-list">
        <li v-for="todo in todos" :key="todo.id">
            {{ todo.title }}
        </li> 
    </ul>
</template>

<script>
export default {
  props: {
    todos: Array
  }
};
</script>
