
<template>
  <div class="grid-container">
    <div class="skills">
      <h4>Skills</h4>
      <ul class="skill-list">
        <li>Java</li>
        <li>HTML</li>
        <li>CSS</li>
        <li>JavaScript</li>
        <li>Spring Boot</li>
        <li>JDBC</li>
        <li>Table Design</li>
        <li>SQL</li>
        <li>PostgreSQL</li>
        <li>E/R diagrams</li>
        <li>Unit Testing (JUnit)</li>
        <li>VUE.js</li>
        <li>Git</li>
        <li>GitHub</li>
        <li>IntelliJ</li>
        <li>Postman</li>
      </ul>
      <h4>Education</h4>
      <ul class="skill-list">
        <li>Tech Elevator boot-camp</li>
        <li>University of Illinois</li>
        <li>Wright State University</li>
      </ul>
    </div>

    <div class="bio">
      <img
        class="head-shot"
        src="../assets/images/EngelHeadShot-TE.jpg"
        alt="head-shot"
      />
      <div class="bio-objects">
        <div
          v-for="(item, index) in bioObjects"
          :key="index"
          class="bio-object"
        >
          <p class="title">{{ item.title }}</p>
          <p class="description">{{ item.description }}</p>
        </div>
      </div>
    </div>

    <div class="projects">
      <h4>Examples</h4>
      <div class="project-images">
        <a
          href="https://regional-weather.netlify.app/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img src="../assets/images/RegionalWeather.png" alt="RegionalWeather"
        /></a>
        <a
          href="https://joke-a-quote-a-day.netlify.app/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img src="../assets/images/Joke-a-Quote-a-Day.png" alt="Jokes"
        /></a>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      bio: "",
      bioObjects: [],
      title: "",
      description: "",
    };
  },
  created() {
    this.fetchBio();
    this.fetchBioObjects();
  },
  methods: {
    fetchBio() {
      const url = new URL(`../assets/text/AboutHome.txt`, import.meta.url);
      fetch(url)
        .then((response) => response.text())
        .then((data) => {
          this.bio = data;
        })
        .catch((error) => {
          console.log.error("problem fetching bio", error);
        });
    },
    fetchBioObjects() {
      const url = new URL(`../assets/text/BioObjects.txt`, import.meta.url);
      fetch(url)
        .then((response) => response.text())
        .then((data) => {
          this.parseBioObjects(data);
        })
        .catch((error) => {
          console.log("error getting bio information", error);
        });
    },
    parseBioObjects(data) {
      const lines = data.split("\n");
      const bioObjects = [];
      let currentObject = {};

      lines.forEach((line) => {
        const [key, value] = line.split(":").map((item) => item.trim());
        if (key && value) {
          currentObject[key] = value;
          if (key === "description") {
            bioObjects.push(currentObject);
            currentObject = {};
          }
        }
      });
      this.bioObjects = bioObjects;
    },
  },
};
</script>

<style scoped>
.bio-text {
  grid-column: 2;
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: white;
  background-color: #3d1f77;
}
.grid-container {
  padding-top: 20px;
  display: grid;
  grid-template-columns: 1fr 3fr 1fr;
  gap: 20px;
  margin: 0;
  width: 100%;
}
.skills,
.projects {
  color: white;
  background-color: #3d1f77;
  padding: 20px;
  border-radius: 5px;
}
.projects {
  grid-column: 3;
}
.skill-list {
  font-size: 12px;
}
.title,
.description {
  font-size: 14px;
}
.head-shot {
  padding-bottom: 15px;
  max-width: 100%;
  height: 400px;
  width: 380px;
}
.bio {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.bio-objects {
  color: white;
  background-color: #3d1f77;
  padding: 20px;
  border-radius: 5px;
  width: 100%;
}
.bio-object {
  margin-bottom: 10px;
}
.project-images {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.project-images a:hover {
  max-width: 100%;
  height: auto;
  border-radius: 5px;
  filter: opacity(40%);
}
img {
  height: 200px;
  width: 200px;
  margin-top: 10px;
}

@media (max-width: 850px) {
  .grid-container {
    grid-template-columns: 1fr; /* This will stack all columns into one */
  }

  .projects {
    grid-column: auto; /* Resetting grid-column to auto to allow stacking */
  }
  .bio {
    order: 1;
  }
  .skills {
    order: 2;
  }
  .projects {
    order: 3;
  }
}
</style>

