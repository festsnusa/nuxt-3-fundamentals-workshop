<template>
  <div class="section">
    <slot name="hero" />
    <h1 class="title">{{ title }}</h1>
    <button @click="fetchItemList">Fetch Data</button>
    <slot name="metrics">
    </slot>
    <ul class="list">
      <slot name="items" :itemList="itemList"></slot>
    </ul>
  </div>
</template>

<script setup>

// import { defineProps, ref } from 'vue'

const props = defineProps({
  itemList: {
    type: Array,
    default: () => []
  },
  itemType: {
    type: String,
    required: true
  },
  title: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['update:itemList'])

function fetchItemList() {
  fetch(`https://jsonplaceholder.typicode.com/${props.itemType}/`)
    .then(response => response.json())
    .then(json => {
      // itemList.value = json
      emit('update:itemList', json)

    })
}
</script>

<style lang="scss" scoped></style>