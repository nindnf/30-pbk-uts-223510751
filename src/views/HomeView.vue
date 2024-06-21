<script setup>
const props = defineProps(["getTasks"]);
</script>

<template>
  <header class="header-background p-5 mb-4 mt-8 rounded-3 text-center">
    <h2><b>Haii.. What Are You To Do?</b></h2>
    <p>list {{ props.getTasks }} </p>
  </header>
</template>

<style>
body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f8f9fa;
  color: #343a40;
}

.header-background {
  background-image: url('@/assets/bgcute.png'); 
  background-size: cover;
  background-position: center;
  width: 100vw;
  height: 100vh;
  padding: 60px;
  border-radius: 8px;
  color: #171111; 
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5); 
}
</style>
