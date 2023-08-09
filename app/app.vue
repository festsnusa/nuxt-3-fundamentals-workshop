<template>
  <h1>Photo Gallery</h1>
  <button @click="fetchPhotoGallery">fetch data</button>
  <p>{{ numberOfPhotos }} photos ({{ evenAlbums }} even, {{ oddAlbums }} odds)</p>
  <ul>
    <li v-for="photo in photoGallery" :key="`photo-id-${photo.id}`">
      <img :src="photo.thumbnailUrl" alt="">
    </li>
  </ul>
</template>

<script>
import { defineNuxtComponent } from 'nuxt/app';

export default defineNuxtComponent({
  data: () => ({
    photoGallery: [],
  }),
  computed: {
    numberOfPhotos() {
      return this.photoGallery.length
    },
    evenAlbums() {
      return this.photoGallery.filter(item => item.albumId % 2 === 0).length
    },
    oddAlbums() {
      return this.photoGallery.filter(item => item.albumId % 2 !== 0).length
    },
  },
  methods: {
    fetchPhotoGallery() {
      fetch('https://jsonplaceholder.typicode.com/photos/')
        .then(response => response.json())
        .then(json => {
          this.photoGallery = json
        })
    }
  }
})
</script>

<style></style>
