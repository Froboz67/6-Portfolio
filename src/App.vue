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
  font-size: clamp(1.25rem, 2vw, 1.75rem);
}

header {
  line-height: 1.5;
  width: 100%;
  max-height: 100vh;
  display: flex;
  justify-content: space-between;
  background-color: #3a334d;
  border-radius: 5px;
}

@media (max-width: 800px) {
  header {
    padding-top: 10px;
    flex-direction: column;
    align-items: center;
  }
  nav {
    display: flex;
    justify-content: center;
    padding-top: 10;
    width: 100%;
  }
  nav ul {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: 10px;
    padding: 0;
    margin: 0;
    list-style: none;
  }
  ul {
    align-items: center;
  }
  nav li {
    margin: 5px 0;
  }
}
</style>
