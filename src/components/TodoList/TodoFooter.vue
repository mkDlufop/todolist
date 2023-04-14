<template>
  <div v-show="todos.length">
    <label>
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成 {{ doneTotal }}</span>
      /全部 {{ todos.length }}
    </span>
    <button @click="deleteDone">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  props: ["todos", "checkAll", "deleteDone"],
  computed: {
    doneTotal() {
      const x = this.todos.reduce((pre, current) => {
        return pre + (current.done ? 1 : 0);
      }, 0);
      return x;
    },
    isAll: {
      get() {
        return this.todos.length === this.doneTotal && this.todos.length > 0;
      },
      set(value) {
        this.checkAll(value);
      },
    },
  },
};
</script>