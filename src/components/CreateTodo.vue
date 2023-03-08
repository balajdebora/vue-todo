<script setup>
import { ref } from 'vue'

const props = defineProps({
  todos: {
    type: Array
  }
})

const newTodo = ref({
  name: '',
  category: null
})

const addNewTodo = () => {
  if (newTodo.value.name && newTodo.value.category) {
    props.todos.push({
      content: newTodo.value.name,
      category: newTodo.value.category,
      done: false,
      createAt: new Date().getTime()
    })

    removeNewTodo()
  }
}

const removeNewTodo = () => {
  newTodo.value.name = ''
  newTodo.value.category = null
}
</script>

<template>
  <section class="create-todo">
    <h3>CREATE A TODO</h3>
    <form @submit.prevent="addNewTodo">
      <h4>What's on your todo list?</h4>
      <input type="text" placeholder="e.g: Make a video" v-model="newTodo.name" class="add-todo" />
      <h4>Pick a category</h4>
      <div class="options">
        <label>
          <input type="radio" name="category" value="business" v-model="newTodo.category" />
          <span class="bubble business"></span>
          <div>Business</div>
        </label>
        <label>
          <input type="radio" name="category" value="personal" v-model="newTodo.category" />
          <span class="bubble personal"></span>
          <div>Personal</div>
        </label>
      </div>

      <input type="submit" value="Add todo" class="btn" />
    </form>
  </section>
</template>
