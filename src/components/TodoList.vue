<template>
  <div class="body">
    <section class="create-todo">
      <h3>APA YANG KAMU INGIN LAKUKAN HARI INI</h3>
      <form @submit.prevent="addTodo">
        <h4>MASUKAN KEGIATAN</h4>
        <input type="text" placeholder="Masukkan kegiatan" v-model="inputContent" />
        <h4>Pilih kategori:</h4>
        <div class="options">
          <label>
            <input type="radio" name="category" value="home" v-model="inputCategory" />
            <span class="bubble home"></span>
            <div>Rumah</div>
          </label>
          <label>
            <input type="radio" name="category" value="assignment" v-model="inputCategory" />
            <span class="bubble task"></span>
            <div>Tugas</div>
          </label>
          <label>
            <input type="radio" name="category" value="work" v-model="inputCategory" />
            <span class="bubble work"></span>
            <div>Kerja</div>
          </label>
        </div>
        <button type="submit">Submit</button>
      </form>
      <div class="todo-list">
        <table>
          <thead>
            <tr>
              <th>Kegiatan</th>
              <th>Kategori</th>
              <th>Aksi</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="todo in todosAsc" :key="todo.createdAt" :class="`todo-item ${todo.done ? 'done' : ''}`">
              <td>{{ todo.content }}</td>
              <td>{{ todo.category }}</td>
              <td>
                <button class="delete" @click="removeTodo(todo)">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch } from 'vue'

const todos = ref([])
const inputContent = ref('')
const inputCategory = ref(null)

const todosAsc = computed(() => todos.value.slice().sort((a, b) => b.createdAt - a.createdAt))

const addTodo = () => {
  if (inputContent.value.trim() === '' || inputCategory.value === null) {
    return
  }

  todos.value.push({
    content: inputContent.value,
    category: inputCategory.value,
    done: false,
    createdAt: new Date().getTime()
  })

  inputContent.value = ''
  inputCategory.value = null
}

const removeTodo = todo => {
  todos.value = todos.value.filter(t => t !== todo)
}

watch(todos, newVal => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, { deep: true })

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})
</script>

<style scoped>
.body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-image: url('https://png.pngtree.com/thumb_back/fh260/background/20231230/pngtree-elegant-gold-accented-black-abstract-background-texture-image_13886480.png');
  background-size: cover;
  background-position: center;
  padding: 20px;
}

.create-todo {
  background: rgba(0, 0, 0, 0.7);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  max-width: 600px;
  width: 100%;
  color: white;
  font-family: 'Oswald', sans-serif;
}

.create-todo h3 {
  font-size: 30px;
  font-weight: bold;
  margin-bottom: 20px;
}

.create-todo h4 {
  margin: 10px 0;
  font-size: 20px;
}

.create-todo form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.create-todo input[type="text"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  border: none;
  font-size: 16px;
}

.create-todo .options {
  display: flex;
  justify-content: center;
  margin: 10px 0;
}

.create-todo .options label {
  margin: 0 10px;
  display: flex;
  align-items: center;
  cursor: pointer;
}

.create-todo .options input[type="radio"] {
  display: none;
}

.create-todo .options .bubble {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  margin-right: 10px;
  border: 2px solid transparent;
  transition: all 0.3s;
}

.create-todo .options input[type="radio"]:checked + .bubble {
  border-color: #d61414;
}

.create-todo .options .home { background: #ffcccb; }
.create-todo .options .task { background: #ccffcc; }
.create-todo .options .work { background: #ccccff; }

button[type="submit"] {
  padding: 10px 20px;
  border: none;
  background: #007bff;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  transition: background 0.3s;
  font-family: 'Oswald', sans-serif;
}

button[type="submit"]:hover {
  background: #0056b3;
}

.todo-list {
  width: 100%;
  max-width: 600px;
  margin: 20px auto;
  text-align: center;
}

.todo-list table {
  width: 100%;
  border-collapse: collapse;
  font-family: 'Oswald', sans-serif;
  background-color: #fff;
}

.todo-list th, .todo-list td {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.todo-list th {
  background-color: #080808;
}

.todo-list tr:hover {
  background-color: #f5f5f5;
}

.todo-list .todo-item.done {
  background: #e0ffe0;
}

.todo-list .todo-item .actions .delete {
  background: transparent;
  border: none;
  color: #dc3545;
  cursor: pointer;
  transition: color 0.3s;
}

.todo-list .todo-item .actions .delete:hover {
  color: #c82333;
}
</style>
