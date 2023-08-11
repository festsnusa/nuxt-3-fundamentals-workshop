<script setup>
import { ref, computed } from 'vue'

const route = useRoute()

const filteredTodoList = computed(() => {
  return (route.query.completed) ? completedItems.value : remainingItems.value
})

const todoList = ref([])

const completedItems = computed(() => {
  return todoList.value.filter(item => item.completed)
})

const remainingItems = computed(() => {
  return todoList.value.filter(item => !item.completed)
})
</script>

<template>
  <NuxtLayout name="todo">
    <div class="section">
      <h1 class="title">This is Todo Viewer</h1>
      <NuxtPage v-if="route.params.id" />
      <BaseDisplay v-else title="Todo Viewer" v-model:itemList="todoList">
        <template v-slot:hero> </template>

        <template v-slot:metrics>
          {{ completedItems.length }} completed |
          {{ remainingItems.length }} remaining
        </template>
        <template v-slot:items>
          <li v-for="todo in filteredTodoList" :key="`todo-id-${todo.id}`">
            <input type="checkbox" :checked="todo.completed"> {{ todo.title }}
            <NuxtLink :to="`/display/todos/${todo.id}`">{{ todo.title }}</NuxtLink>
          </li>
        </template>
      </BaseDisplay>

    </div>
  </NuxtLayout>
</template>

<style lang="scss"></style>
