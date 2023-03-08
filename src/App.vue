<script setup>
import { ref, watch, onMounted } from 'vue'

import Greeting from './components/Greeting.vue'
import CreateTodo from './components/CreateTodo.vue'
import TodoList from './components/TodoList.vue'

const todos = ref([])

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})

watch(
  todos,
  (newTodo) => {
    localStorage.setItem('todos', JSON.stringify(newTodo))
  },
  { deep: true }
)

const removeTodo = (todo) => {
  todos.value = todos.value.filter((item) => item !== todo)
}
</script>

<template>
  <main class="wrapper">
    <Greeting />
    <div class="todo-container">
      <CreateTodo :todos="todos" />
      <TodoList :todos="todos" :removeTodo="removeTodo" />
    </div>
  </main>
</template>
