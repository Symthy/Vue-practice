<template>
  <div>
    <h1 class="app_title">Todo アプリ (Vue practice)</h1>
    <TodoSearch></TodoSearch>
    <TodoItem></TodoItem>
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
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";
.app_title {
  text-align: left;
  @extend .hp_mar_l40;
}
</style>
