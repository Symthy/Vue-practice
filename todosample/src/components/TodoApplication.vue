<template>
  <div>
    <input type="text" v-model="message" />
    <textarea v-model="message"></textarea>
    <p>{{ message }}</p>
    <TodoSearch></TodoSearch>
  </div>
</template>

<script>
import TodoSearch from "./TodoSearch.vue";

export default {
  name: "TodoApplication",
  components: {
    TodoSearch,
  },
  data() {
    return {
      message: "Todo Application Sample",
    };
  },
};
</script>

<style lang="scss" scoped></style>
