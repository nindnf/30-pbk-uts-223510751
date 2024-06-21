<template>
  <div id="app">
    <q-layout view="hHh lpR fFf">
      <q-header elevated class="custom-navbar">
        <q-toolbar>
          <router-link to="/" exact-active-class="active" class="q-item" exact>
            <q-item-label>Home</q-item-label>
          </router-link>
          <router-link to="/forms" exact-active-class="active" class="q-item" exact>
              <q-item-label>Todos</q-item-label>
          </router-link>
          <router-link to="/posts" exact-active-class="active" class="q-item" exact>
            <q-item-label>Post</q-item-label>
          </router-link>
          <router-link to="/albums" exact-active-class="active" class="q-item" exact>
            <q-item-label>Album</q-item-label>
          </router-link>
        </q-toolbar>
      </q-header>
      
      <q-page-container>
        <router-view />
      </q-page-container>
    </q-layout>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
/* Style untuk mengubah warna navbar */
.custom-navbar {
  background-color: #4dbebb; /* Warna latar belakang navbar */
  color: #000000; /* Warna teks navbar */
}

.custom-navbar .q-toolbar {
  display: flex;
  justify-content: center; /* Center the navbar content */
}

.custom-navbar .q-item {
  margin: 0 10px;
}

.custom-navbar .q-item-label {
  color: #ffffff; /* Warna teks link */
  font-weight: bold;
}

.custom-navbar .q-item:hover .q-item-label {
  color: #ffcc00; /* Warna teks link saat di-hover */
}

.custom-navbar .active .q-item-label {
  color: #ffcc00; /* Warna teks link aktif */
}
</style>
