<template>
  <section class="main">
    <input v-model="isAll" id="toggle-all" class="toggle-all" type="checkbox" />
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- 当任务已完成，可以给 li 加上 completed 类，会让元素加上删除线 -->
      <li :class="{ completed: item.flag }" v-for="item in list" :key="item.id">
        <div class="view">
          <input
            class="toggle"
            type="checkbox"
            :checked="item.flag"
            @change="handleChange(item.id, $event)"
          />
          <label>{{ item.title }}</label>
          <button class="destroy" @click="handleDel(item.id)"></button>
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  name: "TodoMain",
  props: {
    list: {
      type: Array,
      required: true,
    },
  },
  methods: {
    handleDel(id) {
      // console.log(id);
      this.$emit("delTodo", id);
    },
    handleChange(id, e) {
      // console.log(id, e);
      this.$emit("editTodo", id, e.target.checked);
    },
  },
  computed: {
    isAll: {
      get() {
        return this.list.every((item) => item.flag === true);
      },
      set(newValue) {
        this.$emit("changeAll", newValue);
      },
    },
  },
};
</script>

<style></style>
