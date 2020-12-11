<template>
  <div>
    <ul class="todo_list" v-if="hasTodo">
      <li class="todo_item" v-for="todo in this.todoList" :key="todo.id">
        <div class="todo_item_done" v-if="todo">
          <input v-model="todo.isDone" type="checkbox" />
        </div>
        <div class="todo_item_content">
          <div class="todo_item_date">
            {{ new Date(todo.dateTime).toString() }}
          </div>
          <h3 class="todo_item_title">{{ todo.title }}</h3>
          <div class="todo_item_detail" v-if="todo.detail">
            {{ todo.detail }}
          </div>
          <ul class="todo_item_categories" v-if="hasCategory(todo)">
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
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todoList: {
      type: Array,
      default: function () {
        return [];
      },
      required: true,
    },
  },
  computed: {
    hasTodo() {
      return this.todoList.length > 0;
    },
    hasCategory() {
      return (todo) => {
        if (todo.categoryList) {
          return todo.categoryList.length > 0;
        }
        return false;
      };
    },
  },
};
</script>

<style></style>
