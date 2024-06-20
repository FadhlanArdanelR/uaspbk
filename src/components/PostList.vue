<template>
  <section class="post-section">
    <h2>Postingan Pengguna</h2>
    <div class="select-user">
      <label>Pilih Pengguna:</label>
      <select v-model="selectedUser" @change="fetchPosts" class="select-box">
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
    </div>
    <div v-if="posts.length > 0" class="user-posts">
      <h3 style="color:black">Postingan Pengguna: {{ selectedUserName }}</h3>
      <table class="post-table">
        <thead>
          <tr>
            <th>Judul</th>
            <th>Isi</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post in posts" :key="post.id">
            <td>{{ post.title }}</td>
            <td>{{ post.body }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const selectedUser = ref(null)
const users = ref([])
const posts = ref([])
const selectedUserName = ref('')

const fetchUsers = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    users.value = await response.json()
  } catch (error) {
    console.error('Error fetching users:', error)
  }
}

const fetchPosts = async () => {
  if (!selectedUser.value) return
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`)
    posts.value = await response.json()
    selectedUserName.value = users.value.find(user => user.id === selectedUser.value)?.name || ''
  } catch (error) {
    console.error('Error fetching posts:', error)
  }
}

onMounted(fetchUsers)
</script>

<style scoped>
.post-section {
  margin-top: 20px;
  background-color: rgb(253, 253, 253);
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 800px;
  margin: 0 auto;
}

.select-user {
  margin-bottom: 20px;
}

.select-box {
  padding: 8px 12px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #0a0a0a;
  transition: border-color 0.3s, background-color 0.3s;
  width: 100%;
  max-width: 300px;
}

.select-box:focus {
  outline: none;
  border-color: #007bff;
  background-color: white;
}

.user-posts {
  margin-top: 20px;
}

.post-table {
  width: 100%;
  border-collapse: collapse;
}

.post-table th,
.post-table td {
  padding: 12px;
  border: 1px solid #000000;
}

.post-table th {
  background-color: #0c0c0c;
}

.post-table td {
  background-color: rgb(10, 10, 10);
}

.post-table tr:hover {
  background-color: #0e0d0d;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-image: url('https://png.pngtree.com/thumb_back/fh260/background/20231230/pngtree-elegant-gold-accented-black-abstract-background-texture-image_13886480.png');
  background-size: cover;
  background-position: center;
  font-family: 'Roboto', sans-serif; /* Menambahkan font family untuk keseragaman */
  overflow-x: hidden; /* Mengatasi scroll horizontal pada gambar latar belakang */
}

h2, h3, label {
  color: #000000;
  text-align: center;
}

.select-user label {
  display: block;
  margin-bottom: 8px;
}

img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
  filter: blur(8px); /* Efek blur pada gambar latar belakang */
}

@media (max-width: 768px) {
  .post-section {
    padding: 15px;
  }
}
</style>
