<template>
  <div class="todo_area">
    <div class="todo_tab">
      <p class="todo_tab_label">Todo</p>
    </div>
    <div class="todo_item hp_pad_r20">
      <div class="ly_todo_element todo_title hp_mar_t20 hp_mar_b5">
        <label class="todo_item_label">タイトル</label>
        <input
          class="todo_title_input hp_mar_r20"
          v-model.trim.lazy="todoTitle"
          type="text"
        />
      </div>
      <div class="ly_todo_element todo_detail hp_mar_t5 hp_mar_b20">
        <label class="todo_item_label">詳細</label>
        <textarea
          class="todo_detail_input hp_mar_r20"
          v-model.trim.lazy="todoDetail"
        ></textarea>
      </div>
      <div class="ly_todo_element todo_category">
        <p class="todo_item_label">カテゴリ</p>
        <form class="todo_category_input" @submit.prevent="createCategory">
          <input class="hp_mar_r20" v-model.trim="categoryName" type="text" />
          <button type="submit" :disabled="!isCanCreateCategory">カテゴリ追加</button>
        </form>
      </div>

      <ul class="todo_category_list">
        <li
          v-for="category in categoryList"
          :key="category"
          class="todo_category_item hp_pad_r5"
        >
          <label :for="'category-' + category">
            <input
              v-model="todoCategories"
              type="checkbox"
              :id="'category-' + category"
              :value="category"
            />
            {{ category }}
          </label>
        </li>
      </ul>
      <div class="ly_todo_element todo_action">
        <form class="hp_mar_tb10 hp_mar_r20" @submit.prevent="createTodo">
          <button type="submit" :disabled="!isCanCreateTodo">Todo作成</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    propTodoList: {
      type: Array,
      default: () => [],
      required: true,
    },
  },
  data() {
    return {
      todoTitle: "",
      todoDetail: "",
      categoryName: "",
      todoList: this.propTodoList,
      todoCategories: [],
      categoryList: [],
    };
  },
  computed: {
    isCanCreateTodo() {
      return this.todoTitle !== "";
    },
    isCanCreateCategory() {
      return this.categoryName !== "" && this.isNotExsitsCategory;
    },
    isNotExsitsCategory() {
      return this.categoryList.indexOf(this.categoryName) < 0;
    },
    hasTodo() {
      return this.todoList.length > 0;
    },
  },
  watch: {
    todoList: {
      handler(next) {
        window.localStorage.setItem("todoList", JSON.stringify(next));
      },
      deep: true,
    },
    categoryList: {
      handler(next) {
        window.localStorage.setItem("categoryList", JSON.stringify(next));
      },
      deep: true,
    },
  },
  methods: {
    createTodo() {
      if (!this.isCanCreateTodo) {
        return;
      }
      this.todoList.push({
        id: "task-" + Date.now(),
        title: this.todoTitle,
        detail: this.todoDetail,
        categoryList: this.todoCategories,
        dateTime: Date.now(),
        isDone: false,
      });
      this.todoTitle = "";
      this.todoDetail = "";
      this.todoCategories = [];
      this.$emit("create-todo", this.todoList);
    },
    createCategory() {
      if (!this.isCanCreateCategory) {
        return;
      }
      this.categoryList.push(this.categoryName);
      this.categoryName = "";
    },
  },
  created() {
    const todoListJson = window.localStorage.getItem("todoList") ?? [];
    const categoryListJson = window.localStorage.getItem("categoryList") ?? [];
    if (this.todoList && this.todoList.length > 0) {
      this.todoList = JSON.parse(todoListJson);
    }
    if (this.categoryList && this.categoryList.length > 0) {
      this.categoryList = JSON.parse(categoryListJson);
    }
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";

.todo_tab {
  width: 95%;
  max-width: 1080px;
  margin: auto; // 中央配置

  .todo_tab_label {
    background-color: #ffc;
    width: 80px;
    height: 20px;
    padding-top: 3px;
    // 外枠
    border: 1px solid rgba(0, 0, 0, 0.3);
    border-bottom: transparent; // 下辺を透明
    border-top-left-radius: 6px;
    border-top-right-radius: 6px;

    text-align: center;
    margin-bottom: -1px;
    margin-left: -1px;
  }
}

.todo_item {
  width: 95%;
  max-width: 1080px;
  margin: auto; // 中央配置

  display: flex;
  // 中身縦並び
  flex-direction: column;
  flex-wrap: wrap;
  // 中身中央寄せ
  justify-content: center;
  align-items: center;

  // 外枠
  border: 1px solid rgba(0, 0, 0, 0.3);
}

.ly_todo_element {
  // 中央寄せ
  display: flex;
  justify-content: center;
  align-items: center;

  // 横幅指定
  width: 100%;
  max-width: 1080px;
}

.todo_item_label {
  flex-basis: 120px;
  @extend .hp_pad_l20;
  text-align: left;
}
.todo_title_input {
  height: 20px;
  flex-basis: 100%;
}
.todo_detail_input {
  height: 40px;
  flex-basis: 100%;
}

.todo_category {
  text-align: left;

  .todo_category_input {
    flex-basis: 100%;
  }
}

.todo_category_list {
  margin: 0;
  width: 100%;
  max-width: 1080px;
  display: flex;
  flex-wrap: wrap;
  // justify-content: flex-start;
  // align-items: start;

  .todo_category_item {
    border: 1px solid rgba(0, 0, 0, 1);
    border-radius: 3px;
    @extend .hp_mar_l20;
  }

  ul,
  li {
    list-style-type: none;
  }
}

.todo_action {
  justify-content: flex-end;
  form {
    @extend .hp_mar_tb10, .hp_mar_r20;
  }
}
</style>
