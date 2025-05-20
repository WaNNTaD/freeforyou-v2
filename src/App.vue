<script setup>
// App.vue avec composition API
</script>

<template>
  <router-view v-slot="{ Component }">
    <transition name="page" mode="out-in">
      <component :is="Component" />
    </transition>
  </router-view>
</template>

<style>
/* Styles globaux qui s'appliqueront à toute l'application */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.page-enter-active,
.page-leave-active {
  transition: opacity 0.3s ease;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
}

body {
  margin: 0;
  overflow-x: hidden;
  background-color: #240046;
  font-family: 'Poppins', sans-serif;
  color: white;
}

h1, h2, h3, h4 {
  font-family: 'Permanent Marker', cursive;
}

/* Classes utilitaires */
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.section {
  padding: 80px 0;
  position: relative;
}

@media (max-width: 768px) {
  .section {
    padding: 50px 0;
  }
}
</style>
