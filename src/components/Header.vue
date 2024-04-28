<script setup>
const props = defineProps(["getTasks"]);
</script>

<template>
  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Haii.. What Are You To Do?</h1>
    <p>list {{ props.getTasks }} </p>
  </header>
</template>

<style>
.header {
  background-color: rgba(255, 255, 255, 0.5); /* Untuk latar belakang transparan */
}
</style>