<template>
  <div class="album-container">
    <h2>Albums</h2>
    <div v-if="albums.length">
      <table class="album-table">
        <tbody>
          <tr v-for="album in albums" :key="album.id" @click="viewAlbum(album.id)" class="album-item">
            <td class="album-id">{{ album.id }}</td>
            <td class="album-title">{{ album.title }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-else class="no-albums">
      <p>No albums available.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useAlbumsStore } from '../stores/albums'
import { useRouter } from 'vue-router'

const albumsStore = useAlbumsStore()
const albums = ref([])
const router = useRouter()

const fetchAlbums = async () => {
  await albumsStore.fetchAlbums()
  albums.value = albumsStore.albums
}

const viewAlbum = (id) => {
  router.push(`/albums/${id}`)
}

onMounted(fetchAlbums)
</script>

<style scoped>
.album-container {
  padding: 20px;
  background: url('https://png.pngtree.com/thumb_back/fh260/background/20231230/pngtree-elegant-gold-accented-black-abstract-background-texture-image_13886480.png') no-repeat center center;
  background-size: cover;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

h2 {
  color: #007bff;
  text-align: center;
  font-weight: bold;
  font-size: 36px;
  font-family: 'Oswald', sans-serif;
  margin-bottom: 20px;
}

.album-table {
  width: 80%;
  max-width: 800px;
  border-collapse: collapse;
  margin: 0 auto;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.album-item {
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
}

.album-item:hover {
  background-color: #007bff;
  color: white;
}

.album-id, .album-title {
  padding: 15px;
  border-bottom: 1px solid #ddd;
  font-size: 18px;
  text-align: left;
}

.album-id {
  font-weight: bold;
  width: 10%;
}

.album-title {
  width: 90%;
  font-family: 'Arial', sans-serif;
}

.no-albums {
  text-align: center;
  margin-top: 20px;
  color: #fff;
  font-size: 20px;
}
</style>
