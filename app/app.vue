<template>
  <img src="./public/todo.jpg" alt="todo">
  <div>
    <button @click="fetchTodoList">fetch data</button>
    <ul>
      <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
        <input type="checkbox" :checked="todo.completed"> {{ todo.title }}
      </li>
    </ul>
  </div>
</template>

<script>
import { defineNuxtComponent } from '#app'

export default defineNuxtComponent({
  data: () => ({
    todoList: []
  }),
  methods: {
    fetchTodoList() {
      fetch('https://jsonplaceholder.typicode.com/todos/')
        .then(response => response.json())
        .then(json => {
          this.todoList = json
        })
    }
  }
})
</script>
