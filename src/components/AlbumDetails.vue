<template>
  <div class="album-container">
    <h2>Choose Album:</h2>
    <select v-model="selectedAlbum" @change="fetchPhotos" class="album-select">
      <option v-for="album in albums" :key="album.id" :value="album.id">{{ album.title }}</option>
    </select>
    <h2>Photos in Album {{ selectedAlbum }}</h2>
    <div v-if="photos.length" class="photos-grid">
      <div v-for="photo in photos" :key="photo.id" class="photo-item">
        <img :src="photo.thumbnailUrl" @click="showPhoto(photo.url)" class="thumbnail">
        <p>{{ photo.title }}</p>
      </div>
    </div>
    <div v-else class="no-photos">
      <p>No photos available.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const selectedAlbum = ref(route.params.id)
const albums = ref([])
const photos = ref([])

const fetchAlbums = async () => {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/albums`)
    albums.value = await response.json()
  } catch (error) {
    console.error('Error fetching albums:', error)
  }
}

const fetchPhotos = async () => {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/albums/${selectedAlbum.value}/photos`)
    photos.value = await response.json()
  } catch (error) {
    console.error('Error fetching photos:', error)
  }
}

const showPhoto = (url) => {
  window.open(url, '_blank')
}

onMounted(() => {
  fetchAlbums()
  fetchPhotos()
})
</script>

<style scoped>
.album-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  background-image: url('https://png.pngtree.com/thumb_back/fh260/background/20231230/pngtree-elegant-gold-accented-black-abstract-background-texture-image_13886480.png');
  background-size: cover;
  background-position: center;
  padding: 20px;
  color: #fff;
}

h2 {
  color: #007bff;
  text-align: center;
  margin-bottom: 20px;
  font-family: 'Oswald', sans-serif;
}

.album-select {
  margin: 0 auto;
  display: block;
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #007bff;
  transition: border-color 0.3s;
}

.album-select:focus {
  outline: none;
  border-color: #0056b3;
}

.photos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 20px;
  margin-top: 20px;
  width: 100%;
  max-width: 800px;
}

.photo-item {
  text-align: center;
  background: rgba(255, 255, 255, 0.8);
  padding: 10px;
  border-radius: 10px;
  transition: transform 0.3s, box-shadow 0.3s;
  cursor: pointer;
}

.photo-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

.thumbnail {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border: 1px solid #007bff;
  border-radius: 5px;
  margin-bottom: 10px;
  transition: border-color 0.3s;
}

.thumbnail:hover {
  border-color: #0056b3;
}

.no-photos {
  text-align: center;
  margin-top: 20px;
}

.no-photos p {
  color: #fff;
  font-size: 18px;
}
</style>
