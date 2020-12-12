<template>
  <div class="app_base">
    <h1 class="app_title">Todo アプリ (Vue practice)</h1>
    <TodoInput :todoList="todos" @create-todo="receiveTodo"></TodoInput>
    <TodoSearch
      :searchOptions="searchOptions"
      @input-search="receiveSearchOption"
    ></TodoSearch>
    <TodoList :todoList="todos" :searchCondition="searchOptions"></TodoList>
    <p>親コンポ：{{ todos }}</p>
    <br />
    <input type="text" v-model="message" />
    <textarea v-model="message"></textarea>
    <p>{{ message }}</p>
  </div>
</template>

<script>
import TodoSearch from "./TodoSearch.vue";
import TodoInput from "./TodoInput.vue";
import TodoList from "./TodoList.vue";

export default {
  name: "TodoApplication",
  components: {
    TodoSearch,
    TodoInput,
    TodoList,
  },
  data() {
    return {
      message: "Todo Application Sample",
      todos: [],
      searchOptions: {},
    };
  },
  methods: {
    receiveTodo(todos) {
      this.todos = todos;
    },
    receiveSearchOption(searchOptions) {
      this.searchOptions = searchOptions;
    },
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
