<template>
  <div class="app_base">
    <h1 class="app_title">Todo アプリ (Vue practice)</h1>
    <TodoItem></TodoItem>
    <TodoSearch></TodoSearch>
    <br />
    <input type="text" v-model="message" />
    <textarea v-model="message"></textarea>
    <p>{{ message }}</p>
  </div>
</template>

<script>
import TodoSearch from "./TodoSearch.vue";
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoApplication",
  components: {
    TodoSearch,
    TodoItem,
  },
  data() {
    return {
      message: "Todo Application Sample",
      categories: [],
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";

.app_base {
  max-width: 1280px;
  margin: auto;
}

.app_title {
  text-align: left;
  @extend .hp_mar_l40;
}
</style>
