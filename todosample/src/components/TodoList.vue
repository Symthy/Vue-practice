<template>
  <div>
    <table class="todo_list">
      <thead>
        <tr>
          <th>No</th>
          <th>Done</th>
          <th>DateTime</th>
          <th>Title</th>
          <th>Detail</th>
          <th>Categories</th>
        </tr>
      </thead>
      <tbody v-if="hasTodo()">
        <tr class="todo_item" v-for="(todo, index) in todoList" :key="todo.id">
          <td>
            {{ index }}
          </td>
          <td class="todo_item_done" v-if="todo">
            <input v-model="todo.isDone" type="checkbox" />
          </td>
          <td class="todo_item_date">
            {{ new Date(todo.dateTime).toLocaleString("ja") }}
          </td>
          <td class="todo_item_title">{{ todo.title }}</td>
          <td class="todo_item_detail" v-if="todo.detail">
            {{ todo.detail }}
          </td>
          <td>
            <ul class="todo_item_categories" v-if="hasCategory(todo)">
              <li
                class="todo_item_category"
                v-for="category in todo.categoryList"
                :key="category"
              >
                {{ category }}
              </li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
    <div>{{ searchCondition }}</div>
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
    },
    searchCondition: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    hasTodo() {
      return () => {
        if (this.todoList) {
          return this.todoList.length > 0;
        }
        return false;
      };
    },
    hasCategory() {
      return (todo) => {
        if (todo.categoryList) {
          return todo.categoryList.length > 0;
        }
        return false;
      };
    },
    filterTodoList() {
      return () => {};
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";

.todo_list {
  margin: auto;
}

.todo_item_categories {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

td {
  border: 1px solid #333;
}

thead {
  background-color: #333;
  color: #fff;
}
</style>
