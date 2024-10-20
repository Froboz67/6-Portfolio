<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header>
    <h1 class="title">Kevin Engel - Full Stack Developer</h1>
    <nav>
      <ul>
        <li><RouterLink to="/">Home</RouterLink></li>
        |
        <li><RouterLink :to="{ name: 'portfolio' }">Projects</RouterLink></li>
        |
        <li>
          <RouterLink :to="{ name: 'resume' }">Resume</RouterLink>
        </li>
      </ul>
    </nav>
  </header>

  <RouterView />
</template>

<style>
body {
  background-color: #1b1027;
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
  color: #271f42;
}

nav ul {
  list-style-type: none;
  display: flex;
  gap: 25px;
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
  position: fixed;
  line-height: 1.5;
  width: 100%;
  max-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #3a334d;
  border-radius: 5px;
  z-index: 1000;
}
</style>
