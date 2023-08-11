<script setup>
import { computed, ref } from 'vue'

const route = useRoute()

const filteredPhotoGallery = computed(() => {
  return (route.query.even) ? photoGallery.value.filter(e => e.albumId % 2 === 0) : photoGallery.value
})

let photoGallery = ref([])

const numberOfPhotos = computed(() => {
  return photoGallery.value.length
})

const evenAlbums = computed(() => {
  return photoGallery.value.filter(item => item.albumId % 2 === 0)
})

const oddAlbums = computed(() => {
  return photoGallery.value.filter(item => !(item.albumId % 2 === 0))
})

function fetchPhotoGallery() {
  fetch('https://jsonplaceholder.typicode.com/photos')
    .then(response => response.json())
    .then(json => {
      photoGallery.value = json
    })
}
</script>

<template>
  <div class="section">
    <h1>Photo Gallery</h1>
    <NuxtPage v-if="route.params.id" />
    <BaseDisplay v-else title="Photo Gallery" itemType="photos" v-model:itemList="photoGallery">
      <template v-slot:hero>
        <p>{{ filteredPhotoGallery.length }} photos</p>
      </template>
      <template v-slot:items>
        <li v-for="photo in filteredPhotoGallery" :key="`photo-id-${photo.id}`">
          <NuxtLink :to="`/display/photos/${photo.id}`">
            <img :src="photo.thumbnailUrl" />
          </NuxtLink>
        </li>
      </template>
    </BaseDisplay>
  </div>

  <!-- <h1>Photo Gallery</h1>
  <button @click="fetchPhotoGallery">Fetch Data</button>
  <p>
    {{ numberOfPhotos }} photos ({{ oddAlbums.length }} odd albums |
    {{ evenAlbums.length }} even albums)
  </p>
  <ul class="photo-gallery-list">

  </ul> -->
</template>

<style lang="scss">
.photo-gallery-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
</style>
