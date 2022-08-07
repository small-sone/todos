<template>
  <header class="header">
    <h1>todos</h1>
    <input
      class="new-todo"
      placeholder="请输入任务名称"
      autofocus
      @keyup.enter="handleEnter"
      v-model="title"
    />
  </header>
</template>

<script>
export default {
  name: "TodoHead",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    handleEnter() {
      if (this.title.trim() === "") {
        alert("请输入内容");
        this.title = "";
        return;
      }

      this.$emit("addTodo", this.title);
      this.title = "";
    },
  },
};
</script>

<style></style>
