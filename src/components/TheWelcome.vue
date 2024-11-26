
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
        <li>SQL</li>
        <li>PostgreSQL</li>
        <li>Trello</li>
        <li>Agile</li>
        <li>Vue.js</li>
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
      <div class="bio-header">
        <RouterLink id="project" :to="{ name: 'portfolio' }">
          <h3 id="project-route">Projects</h3>
          <div class="tile-container">
            <img
              src="../assets/images/2-RegionalWeather.png"
              alt="WeatherApp"
            />
            <img
              src="../assets/images/3-RecordCollection.png"
              alt="WeatherApp"
            />
            <img
              src="../assets/images/4-Joke-a-Quote-a-Day.png"
              alt="WeatherApp"
            />
            <img
              src="../assets/images/5-FullStackToneRow.png"
              alt="WeatherApp"
            />
            <img src="../assets/images/6-DiceRollGames.png" alt="WeatherApp" />
            <img src="../assets/images/7-Portfolio.png" alt="WeatherApp" />
          </div>
        </RouterLink>
      </div>
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
        <div class="video">
          <video controls autoplay loop muted>
            <source :src="homeInVid" type="video/mp4" />
            Your browser does not support video tag.
          </video>
        </div>
        <div class="video">
          <video controls autoplay loop muted>
            <source :src="spotifyVid" type="video/mp4" />
            Your browser does not support video tag.
          </video>
        </div>
        <a
          href="https://2-regionalweather.netlify.app/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img
            src="../assets/images/2-RegionalWeather.png"
            alt="RegionalWeather"
        /></a>
        <a
          href="https://4-joke-a-quote-a-day.netlify.app/"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img src="../assets/images/4-Joke-a-Quote-a-Day.png" alt="Jokes"
        /></a>
      </div>
    </div>
  </div>
</template>


<script>
import videoFile from "../assets/images/1-SpotifyAPI.mp4";
import videoFile2 from "../assets/images/0-HomeInventoryApp.mp4";

export default {
  data() {
    return {
      bio: "",
      bioObjects: [],
      title: "",
      description: "",
      spotifyVid: videoFile,
      homeInVid: videoFile2,
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
.bio-header {
  padding: 10px;
  width: 100%;
  background-color: #3d1f77;
  justify-content: center;
}
.tile-container {
  display: flex;
  justify-content: space-around;
}
.tile-container img {
  height: 50px;
  width: 50px;
  border-radius: 5px;
}
#project {
  text-decoration: none;
  color: white;
}
#project-route {
  display: flex;
  justify-content: center;
}
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
  justify-items: left;
}
.projects {
  grid-column: 3;
}
.skill-list {
  font-size: 18px;
  color: white;
}
.description {
  font-size: 14px;
  margin-bottom: 0;
}
.title {
  font-size: 16px;
  color: white;
  margin-bottom: 0;
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
.video video {
  height: 200px;
  width: 200px;
  margin-top: 10px;
  display: block;
  border: 1px solid white;
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

