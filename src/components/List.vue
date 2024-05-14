<script setup>
import { defineProps, ref } from 'vue';

const props = defineProps(["tasks"]);
const editingIndex = ref(null);
const editedTaskTitle = ref('');

const editTask = (index) => {
  editingIndex.value = index;
  editedTaskTitle.value = props.tasks[index].title; 
};

const saveTask = (index) => {
  props.tasks[index].title = editedTaskTitle.value; 
  editingIndex.value = null; 
};

const deleteTask = (index) => {
  props.tasks.splice(index, 1);
};
</script>

<template>
 <ul class="mt-4 list-group">
  <li class="list-group-item" v-for="(task, index) in props.tasks" :key="task.id">
    <input
      @change="(event) => (task.finished = event.target.checked)"
      :checked="task.finished"
      :id="task.id"
      type="checkbox"
    />
    <!-- Tampilkan input teks saat sedang dalam mode pengeditan -->
    <template v-if="editingIndex === index">
      <input
        v-model="editedTaskTitle"
        @keyup.enter="saveTask(index)"
        @keyup.esc="cancelEdit"
        class="form-control"
      />
      <button @click="saveTask(index)" class="btn btn-sm btn-success mx-2">Save</button>
      <button @click="cancelEdit" class="btn btn-sm btn-secondary">Cancel</button>
    </template>
    <!-- Tampilkan label teks jika tidak dalam mode pengeditan -->
    <template v-else>
      <label :class="{ done: task.finished }" :for="task.id" class="ms-3">{{ task.title }}</label>
      <button @click="editTask(index)" class="btn btn-sm btn-primary mx-2">Edit</button>
      <button @click="deleteTask(index)" class="btn btn-sm btn-danger">Delete</button>
    </template>
  </li>
</ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
