<template>
  <div class="container">
    <!-- Tombol untuk menampilkan/menyembunyikan postingan -->
    <button @click="toggleShowingPosts" class="btn primary">
      {{ showingPosts ? 'Sembunyikan Postingan' : 'Tampilkan Postingan' }}
    </button>
    <!-- Tombol untuk menambahkan tugas -->
    <button @click="toggleShowingTodos" class="btn secondary">
      {{ showingTodos ? 'Sembunyikan Todo' : 'Tampilkan Todo' }}
    </button>

    <!-- Jika tombol "Tampilkan Postingan" diklik -->
    <div v-if="showingPosts" class="posts-container">
      <!-- Select untuk memilih pengguna -->
      <select v-model="selectedUser">
        <option value="">Pilih Pengguna</option>
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>

      <!-- List postingan -->
      <ul v-if="selectedUser" class="post-list">
        <li v-for="post in userPosts" :key="post.id" class="post-item">{{ post.title }}</li>
      </ul>
    </div>

    <!-- Komponen Form untuk menambahkan todo -->
    <component :is="showAddTodoForm ? Form : ''" @submit="handleSubmit" />

    <div>
    <Form :tempTask="tempTask" :editTempTask="editTempTask" />
  </div>
  <div>
<!-- Komponen List -->
<List :tasks="tasks" />
</div>
  </div>

<Header />
</template>

<script setup>
import { ref, watch } from 'vue';
import Form from './components/Form.vue';
import List from './components/List.vue'
import Header from './components/Header.vue'; 

// State
const users = ref([]);
const selectedUser = ref("");
const userPosts = ref([]);
const showingPosts = ref(false);
const showAddTodoForm = ref(false);
const todos = ref([]);
const tempTodo = ref("");
const showingTodos = ref(false);
const tempTask = ref('');

// Fungsi untuk menambahkan tugas ke dalam tasks
const handleTaskAdded = (task) => {
  tasks.value.push(task);
};

const editTempTask = (value) => {
  tempTask.value = value;
};
// Methods
const fetchUsers = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    users.value = await response.json();
  } catch (error) {
    console.error('Error Fetching Users:', error);
  }
};

const fetchUserPosts = async () => {
  if (!selectedUser.value) return;
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
    userPosts.value = await response.json();
  } catch (error) {
    console.error('Error Fetching User Posts:', error);
  }
};

const toggleShowingPosts = () => {
  showingPosts.value = !showingPosts.value;
  if (showingPosts.value) {
    fetchUsers();
  }
};

const openAddTodoForm = () => {
  showAddTodoForm.value = true;
};

const handleSubmit = async () => {
  try {
    // Example of handling form submission
    const response = await fetch('https://jsonplaceholder.typicode.com/todos', {
      method: 'POST',
      body: JSON.stringify({
        userId: selectedUser.value,
        title: tempTodo.value,
        completed: false // You can change this value as needed
      }),
      headers: {
        'Content-type': 'application/json; charset=UTF-8',
      },
    });
    const data = await response.json();
    console.log('Todo added:', data);
    
    // Clear the temporary todo after submission
    tempTodo.value = '';
  } catch (error) {
    console.error('Error adding todo:', error);
  }
};

const toggleShowingTodos = () => {
  showAddTodoForm.value = !showAddTodoForm.value; // Toggle nilai showAddTodoForm
};

// Watch selectedUser changes and fetch user posts
watch(selectedUser, () => {
  fetchUserPosts();
});

</script>




<style>
body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f8f9fa;
  color: #343a40;
}

.container {
  margin: 0;
  padding: 20px;
  background-image: url('./assets/bgcute.png');
  background-size: cover;
  background-position: center;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #333;
}

button.btn {
  margin: 10px;
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

button.btn:hover {
  background-color: #0056b3;
  transform: translateY(-2px);
}

button.btn.primary {
  background-color: #007bff;
}

button.btn.primary:hover {
  background-color: #0056b3;
}

button.btn.secondary {
  background-color: #6c757d;
}

button.btn.secondary:hover {
  background-color: #5a6268;
}

.posts-container {
  margin-top: 20px;
  width: 80%;
}

form {
  margin: 20px 0;
  width: 80%;
  max-width: 400px;
  background: rgba(255, 255, 255, 0.9);
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.form-control {
  margin-bottom: 10px;
  padding: 10px;
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.col {
  flex: 1;
  margin: 5px;
}

.col-md-2 {
  flex: 0 0 16.6667%;
  max-width: 16.6667%;
  margin-right: 10px;
}

.post-list, .todo-list {
  list-style: none;
  padding: 0;
  margin: 20px 0;
  width: 80%;
  max-width: 600px;
}

.post-item, .todo-item {
  background: rgba(255, 255, 255, 0.8);
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 4px;
  transition: background-color 0.3s ease, transform 0.2s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.post-item:hover, .todo-item:hover {
  background-color: #e9ecef;
  transform: translateY(-2px);
}

.new-todo-container {
  background: rgba(255, 255, 255, 0.9);
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-top: 20px;
}
</style>
