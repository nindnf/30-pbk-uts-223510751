<script setup>
const props = defineProps([
  "registerTask",
  "tempTask",
  "changeFilter",
  "editTempTask",
]);
</script>

<template>
  <form @submit.prevent="props.registerTask">
    <div class="row">
      <div class="col">
        <input
          :value="props.tempTask"
          @change="props.editTempTask"
          type="text"
          placeholder=""
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
