<template>
  <div>
    <ul class="todo_list" v-if="hasTodo">
      <li class="todo_item" v-for="todo in todoList" :key="todo.id">
        {{ todo }}
      </li>
      <div class="todo_item_done">
        <input v-model="todo.done" type="checkbox" />
      </div>
      <div class="todo_item_content">
        <div class="todo_item_date">
          {{ new Date(todo.dateTime).toString() }}
        </div>
        <h3 class="todo_item_title">{{ todo.title }}</h3>
        <div class="todo.description">v-if="todo.description">{{ todo.description }}</div>
        <ul class="todo_item_categories" v-if="todo.categories.length > 0">
          <li
            class="todo_item_category"
            v-for="category in todo.categoryList"
            :key="category"
          >
            {{ category }}
          </li>
        </ul>
      </div>
    </ul>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
