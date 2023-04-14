<template>
  <div class="todo-container">
    <TodoHeader :addTodo="addTodo" />
    <TodoBody :todos="todos" />
    <TodoFooter :todos="todos" :checkAll="checkAll" :deleteDone="deleteDone" />
  </div>
</template>

<script>
import TodoHeader from "./TodoHeader.vue";
import TodoBody from "./TodoBody.vue";
import TodoFooter from "./TodoFooter.vue";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoBody,
    TodoFooter,
  },
  data() {
    return {
      todos:
        // [
        //   {id: "001", name:"吃饭", done: true},
        //   {id: "002", name:"洗澡", done: false},
        // ],
        JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem("todos", JSON.stringify(value));
      },
    },
  },
  methods: {
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    checkTodo(id) {
      this.todos.forEach((e) => {
        if (id === e.id) e.done = !e.done;
      });
    },
    updateTodo(id, value) {
      this.todos.forEach((e) => {
        if (e.id === id) {
          e.name = value;
        }
      });
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((e) => {
        return e.id !== id;
      });
    },
    checkAll(done) {
      this.todos.forEach((e) => {
        e.done = done;
      });
    },
    deleteDone() {
      this.todos = this.todos.filter((e) => {
        return !e.done;
      });
    },
  },
  mounted() {
    this.$bus.$on("deleteTodo", this.deleteTodo);
    this.$bus.$on("checkTodo", this.checkTodo);
    this.$bus.$on("updateTodo", this.updateTodo);
    // console.log("vue", this);
  },
  beforeDestroy() {
    this.$bus.$off("deleteTodo");
    this.$bus.$off("checkTodo");
    this.$bus.$off("updateTodo");
  },
};
</script>

<style scoped>
.todo-container {
  width: 600px;
  border: 1px solid;
  border-radius: 8px;
  padding: 10px 39px 10px 5px;
  margin: 0 auto;
}
</style>
