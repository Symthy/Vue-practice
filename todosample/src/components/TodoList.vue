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
            {{ index + 1 }}
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
    <br />
    <p>検索オプション適用後リスト</p>
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
        <tr class="todo_item" v-for="(todo, index) in filterTodoList()" :key="todo.id">
          <td>
            {{ index + 1 }}
          </td>
          <td class="todo_item_done" v-if="todo">
            <input v-model="todo.isDone" type="checkbox" readonly />
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
    <br />
    <p>子コンポ化リスト</p>
    <transition-group name="todo-list" tag="ul" v-if="hasTodo" class="todo-list">
      <TodoItem
        v-for="todo in todoList"
        :key="todo.id"
        :todo="todo"
        v-model:isDone="todo.isDone"
      ></TodoItem>
    </transition-group>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
  props: {
    todoList: {
      type: Array,
      default: function () {
        return [];
      },
    },
    searchCondition: {
      type: Object,
      default: () => {
        return {
          searchWord: "",
          isHideDone: false,
          order: "asc",
        };
      },
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
      return () => {
        const searchWord = this.searchCondition.searchWord;
        const isHideDoneTodo = this.searchCondition.isHideDone;
        const orderTodo = this.searchCondition.order;
        return this.todoList
          .filter((todo) => {
            if (isHideDoneTodo) {
              return todo.isDone;
            }
            return true;
          })
          .filter((todo) => {
            if (searchWord == null || searchWord === "") {
              return true;
            }
            if (
              todo.title.indexOf(searchWord) === -1 &&
              todo.detail.indexOf(searchWord) === -1
            ) {
              return false;
            }
            return true;
          })
          .sort((before, after) => {
            if (orderTodo === "asc") {
              return before.dateTime - after.dateTime;
            }
            return after.dateTime - before.dateTime;
          });
      };
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
  margin: auto 5px auto -15px;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  text-align: left;
}

td {
  border: 1px solid #333;
}

thead {
  background-color: #333;
  color: #fff;
}

.todo-list-enter-from {
  opacity: 0;
  transform: translateX(-20px);
}
.todo-list-leave-to {
  opacity: 0;
  transform: translateX(20px);
}
.todo-list-enter-to,
.todo-list-leave-from {
  opacity: 1;
  transform: translateX(0);
}
.todo-list-enter-active,
.todo-list-leave-active {
  transition: opacity 300ms ease, transform 300ms ease;
}
</style>
