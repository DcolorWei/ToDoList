<template>
  <div class="container"><HomeView /></div>
</template>

<script setup lang="ts">
import HomeView from "./view/HomeView.vue";
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
@media screen and (max-width: 500px) {
  .container {
    width: 100%;
  }
}

@media screen and (min-width: 500px) {
  .container {
    width: 500px;
    max-width: 500px;
    margin: 0 auto;
  }
}
</style>
