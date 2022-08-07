<template>
  <footer class="footer" v-if="list.length > 0">
    <span class="todo-count">
      剩余
      <strong>{{ leftCount }}</strong>
    </span>
    <ul class="filters">
      <li>
        <a
          :class="{ selected: filterType === 'all' }"
          href="#/all"
          @click.prevent="changeFilterType('all')"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: filterType === 'active' }"
          href="#/active"
          @click.prevent="changeFilterType('active')"
          >进行中</a
        >
      </li>
      <li>
        <a
          :class="{ selected: filterType === 'completed' }"
          href="#/completed"
          @click.prevent="changeFilterType('completed')"
          >已完成</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="handleClear">清除已完成</button>
  </footer>
</template>

<script>
export default {
  name: "TodoFoot",
  props: {
    list: {
      type: Array,
      required: true,
    },
    filterType: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      // filterType: "all",
    };
  },
  computed: {
    leftCount() {
      return this.list.filter((item) => item.flag === false).length;
    },
  },
  methods: {
    handleClear() {
      this.$emit("clearComplateTodos");
    },
    changeFilterType(newType) {
      // console.log(newType);
      // this.filterType = newType;
      this.$emit("filterTodo", newType);
    },
  },
};
</script>

<style></style>
