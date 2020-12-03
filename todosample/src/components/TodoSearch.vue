<template>
  <div class="todo_search un_blue">
    <div class="todo_search_box un_pad_all5">
      <label class="todo_search_label un_pad_rl10">キーワード検索</label>
      <input class="todo_search_input un_pad_rl10" type="text" v-model="searchWord" />
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoSearch",
  data() {
    return {
      searchWord: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";

.todo_search_box {
  display: flex;
  justify-content: center;
}
.todo_search_label,
.todo_search_input {
  display: block;
}
</style>
