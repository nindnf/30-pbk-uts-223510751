<template>
  <div id="app">
    <q-layout view="hHh lpR fFf">
      <q-header elevated class="custom-navbar animated-navbar">
        <q-toolbar>
          <q-toolbar-title class="custom-title">
            <h3>✩♬₊˚-ANIN's PROJECT-˚☾⋆⁺₊✧</h3>
          </q-toolbar-title>
          <q-space></q-space>
          <router-link to="/" exact-active-class="active" class="q-item animated-item" exact>
            <q-icon name="home" />
            <q-item-label>Home</q-item-label>
          </router-link>
          <router-link to="/forms" exact-active-class="active" class="q-item animated-item" exact>
            <q-icon name="list_alt" />
            <q-item-label>Todos</q-item-label>
          </router-link>
          <router-link to="/posts" exact-active-class="active" class="q-item animated-item" exact>
            <q-icon name="article" />
            <q-item-label>Post</q-item-label>
          </router-link>
          <router-link to="/albums" exact-active-class="active" class="q-item animated-item" exact>
            <q-icon name="photo_album" />
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
.custom-navbar {
  background: linear-gradient(90deg, rgba(255, 0, 0, 0.5), rgba(255, 165, 0, 0.5), rgba(255, 255, 0, 0.5), rgba(0, 128, 0, 0.5), rgba(0, 0, 255, 0.5), rgba(75, 0, 130, 0.5), rgba(238, 130, 238, 0.5));
  color: #000000; 
  height: 120px; 
  padding: 0 10px;
  transition: background 2s ease-in-out; 
}

@keyframes gradientAnimation {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animated-navbar {
  background-size: 400% 400%;
  animation: gradientAnimation 15s ease infinite;
}

.custom-navbar .q-toolbar {
  display: flex;
  justify-content: space-between; 
  align-items: center; 
  padding: 0;
  height: 100%; 
}

.custom-title h3 {
  margin: 5;
  color: #000000;
  font-size: 2.0rem; 
  font-weight: bold;
  text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.719); /* Tambahkan bayangan teks untuk tampilan lebih baik */
}

.custom-navbar .q-item {
  display: flex;
  align-items: center;
  margin: 0 10px;
  padding: 0 5px; /* Perkecil padding item */
  transition: transform 0.3s ease-in-out; /* Tambahkan animasi transisi transform */
}

.custom-navbar .q-item-label {
  color: #070303; /* Warna teks link */
  font-weight: bold;
  margin-left: 5px; 
}

.custom-navbar .q-item:hover .q-item-label {
  color: #7b765f84; 
}

.custom-navbar .active .q-item-label {
  color: #7b765f84; 
}

.custom-navbar .q-icon {
  font-size: 1.2rem; 
  margin-right: 5px; 
}

.animated-item:hover {
  transform: scale(1.1); 
}
</style>
