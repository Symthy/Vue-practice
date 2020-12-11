<template>
  <div class="app_base">
    <h1 class="app_title">Todo アプリ (Vue practice)</h1>
    <TodoInput :todoList="todos" @create-todo="receiveTodo"></TodoInput>
    <TodoSearch></TodoSearch>
    <TodoList :todoList="todos"></TodoList>
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
    };
  },
  methods: {
    receiveTodo(todos) {
      this.todos = todos;
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
