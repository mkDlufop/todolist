<template>
  <div>
    <label for="todo">代办事项</label><br />
    <input
      id="todo"
      type="text"
      placeholder="请输入代办项"
      v-model="todoValue"
      @keyup.enter="add"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";

export default {
  data() {
    return {
      todoValue: "",
    };
  },
  methods: {
    add() {
      if (!this.todoValue.trim()) return alert("输入不能为空");
      const todoObj = { id: nanoid(), name: this.todoValue, done: false };
      this.addTodo(todoObj);
      this.todoValue = "";
    },
  },
  props: ["addTodo"],
};
</script>