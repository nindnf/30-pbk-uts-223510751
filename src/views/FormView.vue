<template>
  <div class="todo-app">
    <h2 class="title">Silahkan isi form <br> untuk membuat todo list</h2>
    <div class="form-container">
      <form @submit.prevent="registerTask">
        <div class="row">
          <div class="col">
            <input
              v-model="inputTask"
              type="text"
              placeholder="Tambahkan tugas"
              class="form-control form-control-lg"
              required
            />
          </div>
          <div class="col">
            <select class="form-control form-control-lg" v-model="currentFilter">
              <option value="all">All</option>
              <option value="undone">Undone</option>
              <option value="done">Done</option>
            </select>
          </div>
        </div>
        <div class="row mt-2">
          <div class="col">
            <button type="submit" class="btn btn-lg btn-success add-todo-btn">Add To Do</button>
          </div>
        </div>
      </form>

      <ul class="mt-4 list-group">
        <li class="list-group-item" v-for="(task, index) in filteredTasks" :key="task.id">
          <input
            v-model="task.finished"
            :id="task.id"
            type="checkbox"
          />
          <template v-if="editingIndex === index">
            <input
              v-model="editedTaskTitle"
              @keyup.enter="saveTask(index)"
              @keyup.esc="cancelEdit"
              class="form-control"
            />
            <button @click="saveTask(index)" class="btn btn-sm btn-success mx-2 btn-save">Save</button>
            <button @click="cancelEdit" class="btn btn-sm btn-secondary btn-cancel">Cancel</button>
          </template>
          <template v-else>
            <label :class="{ done: task.finished }" :for="task.id" class="ms-3">{{ task.title }}</label>
            <button @click="editTask(index)" class="btn btn-sm btn-primary mx-2 btn-edit">Edit</button>
            <button @click="deleteTask(index)" class="btn btn-sm btn-danger btn-delete">Delete</button>
          </template>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';

const inputTask = ref('');
const tasks = ref(JSON.parse(localStorage.getItem('tasks')) || []);
const editingIndex = ref(null);
const editedTaskTitle = ref('');
const currentFilter = ref('all');

const saveTasksToLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));
};

const registerTask = () => {
  if (inputTask.value.trim() !== '') {
    tasks.value.push({
      id: Date.now(),
      title: inputTask.value,
      finished: false,
    });
    inputTask.value = '';
    saveTasksToLocalStorage();
  }
};

const filteredTasks = computed(() => {
  if (currentFilter.value === 'all') {
    return tasks.value;
  } else if (currentFilter.value === 'undone') {
    return tasks.value.filter(task => !task.finished);
  } else if (currentFilter.value === 'done') {
    return tasks.value.filter(task => task.finished);
  }
  return tasks.value;
});

const editTask = (index) => {
  editingIndex.value = index;
  editedTaskTitle.value = tasks.value[index].title;
};

const saveTask = (index) => {
  tasks.value[index].title = editedTaskTitle.value;
  editingIndex.value = null;
  saveTasksToLocalStorage();
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
  saveTasksToLocalStorage();
};

const cancelEdit = () => {
  editingIndex.value = null;
};

watch(tasks, saveTasksToLocalStorage, { deep: true });
</script>

<style scoped>
.todo-app {
  background-image: url('@/assets/bgcute.png');
  background-size: cover;
  background-position: center;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start; 
  align-items: center;
  padding: 20px;
  color: #000000;
  text-align: center; 
  position: relative; 
  z-index: 0; 
}

.form-container {
  width: 100%;
  max-width: 600px; 
  background-color: rgba(0, 0, 0, 0.5); 
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-top: 10px;
  position: relative;
  z-index: 2; 
}

.list-group-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: rgba(0, 0, 0, 0.6); 
  color: #fff;
  z-index: 2; 
}

.title {
  font-size: 2.5rem; 
  font-weight: bold; 
  text-transform: uppercase; 
  color: #000000;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.4); 
  margin-bottom: 10px; 
  text-align: center; 
  letter-spacing: 1px; 
  z-index: 2; 
}

.row {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  z-index: 2; 
}

.col {
  flex: 1;
  z-index: 2; 
}

.form-control-lg {
  height: calc(1.5em + 1rem + 2px);
  padding: .5rem 1rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: .3rem;
  z-index: 2; 
}

.btn {
  width: 100%;
  height: 50px; 
  font-size: 0.80rem;
  padding: 0.5rem 1rem;
  z-index: 2; 
}

.add-todo-btn {
  width: 100%; 
  z-index: 2; 
}

.mt-4 {
  margin-top: 1rem;
  z-index: 2; 
}

.list-group {
  width: 100%;
  z-index: 2; 
}

.btn-edit {
  color: #fff;
  background-color: #6c757d; 
  border-color: #6c757d; 
  z-index: 2; 
}

.btn-edit:hover {
  background-color: #545b62; 
  border-color: #545b62;
}

.btn-delete {
  color: #fff;
  background-color: #dc3545; 
  border-color: #dc3545; 
  z-index: 2; 
}

.btn-delete:hover {
  background-color: #bd2130; 
  border-color: #b21f2d; 
}

.btn-save {
  color: #fff;
  background-color: #14ff5f;
  border-color: #14ff5f; 
  z-index: 2; 
}

.btn-save:hover {
  background-color: #14ff5f; 
  border-color: #14ff5f; 
}

.btn-cancel {
  color: #fff;
  background-color: #6c757d; 
  border-color: #6c757d; 
  z-index: 2;
}

.btn-cancel:hover {
  background-color: #5a6268; 
  border-color: #545b62; 
}

.btn-success {
  color: #fff;
  background-color: #cb2de7; 
  border-color: #cb2de7; 
  z-index: 2; 
}

.btn-success:hover {
  background-color: #cb2de7;
  border-color: #cb2de7;
}

.done {
  text-decoration: line-through;
}

</style>
