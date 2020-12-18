<template>
  <li class="todo_item">
    <div class="todo_item_done">
      <input :checked="isDone" @change="onChangeTodo" type="checkbox" />
    </div>
    <div class="todo_item_content">
      <div class="todo_item_date">
        {{ new Date(todo.dateTime).toLocaleString("ja") }}
      </div>
      <h3 class="todo_item_title">
        {{ todo.title }}
      </h3>
      <div class="todo_item_detail" v-if="todo.detail">
        {{ todo.detail }}
      </div>
      <ul class="todo_item_categories" v-if="hasCategories">
        <li
          class="todo_item_category"
          v-for="category in todo.categoryList"
          :key="category"
        >
          {{ category }}
        </li>
      </ul>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    isDone: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    hasCategories() {
      return this.todo.categoryList.length > 0;
    },
  },
  methods: {
    onChangeTodo($event) {
      return this.$emit("update:isDone", $event.target.checked);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";
/* .todo-item {
  transition: opacity 300ms ease, transform 300ms ease;
} */
.todo_item,
.todo_item_content {
  display: flex;
  justify-content: center;
  align-items: center;
}

.todo_item_content > * {
  @extend .hp_mar_r10;
  margin-top: auto;
  margin-bottom: auto;
}
.todo_item > * {
  @extend .hp_mar_r10;
}
</style>
