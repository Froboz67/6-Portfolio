<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <h1 class="title">Kevin Engel</h1>
    <nav>
      <RouterLink to="/">Home</RouterLink> |
      <!-- <RouterLink to="/about">About</RouterLink> | -->
      <RouterLink :to="{ name: 'resume' }">Resume</RouterLink> |
      <RouterLink :to="{ name: 'portfolio' }">Portfolio</RouterLink>
    </nav>
  </header>

  <RouterView />
</template>

<style>
body {
  background-color: white;
}

nav {
  color: white;
  padding: 20px;
}
nav a {
  color: white;
  text-decoration: none;
}

nav a:hover {
  color: #ee9b00;
}
RouterLink {
  color: white;
  text-decoration: none;
}

.title {
  color: white;
  padding: 20px;
}

header {
  line-height: 1.5;
  width: 100%;
  max-height: 100vh;
  display: flex;
  justify-content: space-between;
  background-color: #001219;
  border-radius: 5px;
}
</style>
