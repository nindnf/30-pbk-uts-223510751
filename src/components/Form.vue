<template>
  <form @submit.prevent="handleSubmit">
    <div class="row">
      <div class="col">
        <input
          :value="tempTask"
          @input="handleInput"
          type="text"
          placeholder="Tambahkan tugas"
          class="form-control"
          required
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Add To Do</button>
      </div>
      <div class="col-md-2">
        <select class="form-control" @change="handleChangeFilter">
          <option value="todos">All</option>
          <option value="Undone">Undone</option>
          <option value="Done">Done</option>
        </select>
      </div>
    </div>
  </form>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

// Definisikan props yang diterima oleh komponen
const props = defineProps({
  tempTask: String,
  editTempTask: Function
});

// Definisikan emit untuk mengakses event yang diperlukan
const { emit } = defineEmits(['taskAdded']);

// Fungsi untuk menangani submit form
const handleSubmit = () => {
  // Panggil emit untuk melemparkan event taskAdded
  emit('taskAdded', props.tempTask);
};

// Fungsi untuk menangani perubahan input
const handleInput = (event) => {
  // Panggil properti editTempTask jika tersedia
  if (typeof props.editTempTask === 'function') {
    props.editTempTask(event.target.value);
  }
};
</script>



<style scoped>
.row {
  display: flex;
  align-items: center;
  margin-bottom: 20px; /* Increase margin for better spacing */
}

.col {
  flex: 1;
}

.col-md-2 {
  flex: 0 0 25%; /* Increase the width of the form elements */
  max-width: 25%; /* Adjust max-width accordingly */
  margin-right: 20px; /* Increase right margin for better spacing */
}

.form-control {
  width: 100%;
}

.btn {
  width: 100%;
}
</style>