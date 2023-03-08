<script setup>
import { computed } from 'vue'

const props = defineProps({
  todos: {
    type: Array
  },
  removeTodo: {
    type: Function
  }
})

const sort_todos = computed(() =>
  props.todos.sort((a, b) => {
    return b.createAt - a.createAt
  })
)
</script>

<template>
  <section class="todo-list">
    <h3>TODO LIST</h3>
    <div class="list">
      <div v-for="todo in sort_todos" class="todo-item" :class="{ done: todo.done }">
        <label>
          <input type="checkbox" v-model="todo.done" />
          <span :class="`bubble ${todo.category}`"></span>
        </label>
        <div class="todo-content">
          <input type="text" v-model="todo.content" />
        </div>

        <div class="actions">
          <button class="delete" @click="props.removeTodo(todo)">Delete</button>
        </div>
      </div>
    </div>
  </section>
</template>
