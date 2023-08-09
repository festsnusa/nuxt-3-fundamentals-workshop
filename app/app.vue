<script setup>
import PhotoGallery from './components/PhotoGallery.vue'
import TodoViewer from './components/TodoViewer.vue'
</script>

<template>
  <div class="container">
    <div class="section">
      <div class="columns">
        <div class="column">
          <PhotoGallery />
        </div>
        <div class="column">
          <TodoViewer title="Hi!">
            <template v-slot:hero>
              <h2>This works!</h2>
              <img src="./public/todo.jpg" alt="todo">
            </template>
            <template v-slot:metrics="slotProps">
              <strong>{{ slotProps.completed.length }} items completed</strong>
              <h3>This worked!</h3>
            </template>
          </TodoViewer>
        </div>
      </div>
    </div>

  </div>
</template>

<style></style>
