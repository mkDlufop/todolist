<template>
  <div>
    <ul v-for="todo in todos" :key="todo.id">
      <TodoItem :todo="todo" />
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
  props: ["todos"],
};
</script>