<script setup>
const props = defineProps(["getTasks"]);
</script>

<template>
  <header class="p-5 mb-4 mt-8 rounded-3 text-center">
    <h1><b>Haii.. What Are You To Do?</b></h1>
    <p>list {{ props.getTasks }} </p>
  </header>
</template>

