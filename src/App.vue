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
RouterLink {
  color: white;
  text-decoration: none;
}
nav ul {
  list-style-type: none;
  display: flex;
  gap: 15px;
}
nav li {
  margin: 0;
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
  align-items: center;
  background-color: #3a334d;
  border-radius: 5px;
}
</style>
