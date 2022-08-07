<template>
  <section class="todoapp">
    <!-- 头部部分 -->
    <todo-head @addTodo="handleAddTodo" />

    <!-- 主体部分 -->
    <todo-main
      :list="filterList"
      @delTodo="handleDelTodo"
      @editTodo="handleEditTodo"
      @changeAll="handleChangeAll"
    />

    <!-- 底部部分 -->
    <todo-foot
      :list="list"
      @clearComplateTodos="handleClearComplateTodos"
      :filterType="filterType"
      @filterTodo="handleFilterTodo"
    />
  </section>
</template>

<script>
import TodoHead from "@/components/TodoHead.vue";
import TodoMain from "@/components/TodoMain.vue";
import TodoFoot from "@/components/TodoFoot.vue";

export default {
  name: "App",
  components: {
    TodoHead,
    TodoMain,
    TodoFoot,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("101-todos")) || [],
      filterType: "all",
    };
  },
  methods: {
    handleDelTodo(id) {
      // console.log(id);
      this.list = this.list.filter((item) => item.id !== id);
    },
    handleEditTodo(editId, editFlag) {
      // console.log(editId, editFlag);
      const todo = this.list.find((item) => item.id === editId);
      todo.flag = editFlag;
    },
    handleAddTodo(newTodo) {
      const todo = {
        id: +new Date(),
        title: newTodo,
        flag: false,
      };
      // 添加到尾部
      this.list.push(todo);
      // 添加到头部
      // this.list.unshift(todo);
    },
    handleClearComplateTodos() {
      this.list = this.list.filter((item) => item.flag === false);
    },
    handleFilterTodo(newType) {
      this.filterType = newType;
    },
    handleChangeAll(newValue) {
      this.list.forEach((item) => (item.flag = newValue));
    },
  },
  computed: {
    filterList() {
      if (this.filterType === "all") {
        return this.list;
      } else if (this.filterType === "active") {
        return this.list.filter((item) => item.flag === false);
      } else {
        return this.list.filter((item) => item.flag === true);
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(newValue) {
        localStorage.setItem("101-todos", JSON.stringify(newValue));
      },
    },
  },
};
</script>

<style></style>
