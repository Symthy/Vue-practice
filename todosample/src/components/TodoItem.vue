<template>
  <div class="todo_area">
    <div class="todo_tab">
      <p class="todo_tab_label">Todo</p>
    </div>
    <div class="todo_item">
      <div class="todo_title">
        <label class="todo_title_label">タイトル</label>
        <input class="todo_title_input" v-model.trim.lazy="todoTitle" type="text" />
      </div>
      <div class="todo_detail">
        <label class="todo_detail_label">詳細</label>
        <textarea class="todo_detail_input" v-model.trim.lazy="todoDetail" type="text"></textarea>
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
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/utility.scss";

.todo_tab {
  width: 95%;
  max-width: 1080px;
  margin: auto; // 中央配置
}

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

.todo_title,
.todo_detail {
  // 中央寄せ
  display: flex;
  justify-content: center;
  align-items: center;

  // 横幅指定
  width: 100%;
  max-width: 1080px;

  input,
  textarea {
    flex-basis: 100%;
    @extend .hp_mar_r20;
  }
}
.todo_title {
  @extend .hp_mar_t20, .hp_mar_b5;
}
.todo_detail {
  @extend .hp_mar_t5, .hp_mar_b20;
}

.todo_title_label,
.todo_detail_label {
  flex-basis: 120px;
  @extend .hp_mar_l40;
  text-align: left;
}

.todo_title_input {
  height: 20px;
}
.todo_detail_input {
  height: 40px;
}
</style>
