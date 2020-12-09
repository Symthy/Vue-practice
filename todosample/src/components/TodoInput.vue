<template>
  <div class="todo_area">
    <div class="todo_tab">
      <p class="todo_tab_label">Todo</p>
    </div>
    <div class="todo_item">
      <div class="ly_todo_element todo_title hp_mar_t20 hp_mar_b5">
        <label class="todo_item_label">タイトル</label>
        <input class="todo_title_input hp_mar_r20" v-model.trim.lazy="todoTitle" type="text" />
      </div>
      <div class="ly_todo_element todo_detail hp_mar_t5 hp_mar_b20">
        <label class="todo_item_label">詳細</label>
        <textarea class="todo_detail_input hp_mar_r20" v-model.trim.lazy="todoDetail" type="text"></textarea>
      </div>
      <div class="ly_todo_element todo_category">
        <p class="todo_item_label">カテゴリ</p>
        <form class="todo_category_input" @submit.prevent="createCategory">
          <input class="hp_mar_r20" v-model.trim="categoryName" type="text" />
          <button type="submit" :disabled="!isCanCreateCategory">カテゴリ追加</button>
        </form>
      </div>
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
  data() {
    return {
      todoTitle: "",
      todoDetail: "",
      categoryName: "",
      todoList: [],
      categoryList: [],
    };
  },
  computed: {
    isCanCreateTodo() {
      return this.todoTitle !== "";
    },
    isCanCreateCategory() {
      return this.categoryName !== "" && this.isExsitsCategory();
    },
    isExsitsCategory() {
      return this.categories.indexof(this.categoryName) !== -1;
    },
    hasTodo() {
      return this.todoList.length > 0;
    },
  },
  watch: {
    todoList: {
      handler(next, prev) {
        window.localStorage.setItem("todoList", JSON.stringify(next));
      },
      deep: true,
    },
    categoryList: {
      handler(next, prev) {
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
        categories: this.categories,
        dateTime: Date.now(),
        isDone: false,
      });
      this.todoTitle = "";
      this.todoDetail = "";
      this.categories = [];
    },
    createCategory() {
      if (!this.isCanCreateCategory) {
        return;
      }
      this.categories.push(this.categoryName);
      this.categoryName = "";
    },
  },
  created() {
    const todoListJson = window.localStorage.getItem("todoList");
    const categoryListJson = window.localStorage.getItem("categoryList");
    if (todoList) {
      this.todoList = JSON.parse(todoListJson);
    }
    if (categoryList) {
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
  @extend .hp_mar_l40;
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
}
.todo_category_input {
  flex-basis: 100%;
}

.todo_action {
  justify-content: flex-end;
  form {
    @extend .hp_mar_tb10, .hp_mar_r20;
  }
}
</style>
