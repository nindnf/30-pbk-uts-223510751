<script setup>

const props = defineProps({
  registerTask: Function,
  tempTask: String,
  changeFilter: Function,
  editTempTask: Function,
});

const inputTask = ref(props.tempTask);

watch(() => props.tempTask, (newTask) => {
  inputTask.value = newTask;
});
</script>

<template>
  <form @submit.prevent="props.registerTask">
    <div class="row">
      <div class="col">
        <input
          :value="inputTask"
          @input="props.editTempTask"
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
        <select class="form-control" @change="props.changeFilter">
          <option value="todas">All</option>
          <option value="Undone">Undone</option>
          <option value="Done">Done</option>
        </select>
      </div>
    </div>
  </form>
</template>

<style scoped>
.row {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.col {
  flex: 1;
}

.col-md-2 {
  flex: 0 0 25%; /* Perbesar lebar kolom menjadi 25% */
  max-width: 25%; /* Sesuaikan max-width */
  margin-right: 10px;
}

.form-control {
  width: 100%;
}

.btn {
  width: 100%;
}
</style>
