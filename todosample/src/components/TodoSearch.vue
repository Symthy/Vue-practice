<template>
  <div class="todo_search">
    <div class="todo_search_base">
      <div class="todo_search_item">
        <label class="todo_search_label">完了タスク非表示</label>
        <input class="todo_search_input" type="checkbox" v-model="isHideDone" />
      </div>
      <div class="todo_search_item">
        <p class="todo_search_separator">|</p>
      </div>
      <div class="todo_search_item">
        <lable>並び順</lable>
        <select class="todo_search_input" v-model="order">
          <option value="asc">昇順</option>
          <option value="disc">降順</option>
        </select>
      </div>
      <div class="todo_search_item">
        <p class="todo_search_separator">|</p>
      </div>
      <div class="todo_search_item">
        <label class="todo_search_label">キーワード検索</label>
        <input class="todo_search_input" type="text" v-model.trim="searchWord" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoSearch",
  data() {
    return {
      searchWord: "",
      isHideDone: false,
      order: "asc",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";

.todo_search {
  width: 100%;
  max-width: 1280px;

  display: flex;
  justify-content: center;
}

.todo_search_base {
  width: 100%;
  max-width: 1080px;

  display: flex;
  justify-content: flex-start;
  align-items: center;
  @extend .hp_mar_l40;
}

.todo_search_item {
  @extend .hp_mar_all5;
}

.todo_search_input {
  @extend .hp_mar_l5;
}

.todo_search_separator {
  @extend .hp_mar_rl10;
}
</style>
