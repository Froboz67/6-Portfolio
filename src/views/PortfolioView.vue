<template>
  <div>
    <h2>Projects</h2>
    <div class="repos">
      <div class="column" v-for="(project, index) in data" :key="project.id">
        <repo-component
          :title="project.name"
          :htmlUrl="project.html_url"
          :id="project.id"
          :index="index"
        ></repo-component>
      </div>
    </div>
  </div>
</template>

<script>
import repoComponent from "../components/ThePortfolio.vue";
import githubService from "../services/GithubService";

export default {
  components: {
    repoComponent,
  },
  data() {
    return {
      data: [],
    };
  },
  created() {
    githubService.getRepos().then((response) => {
      this.data = response.data.filter((project) => {
        return (
          // When updating titles have to be altered here
          // also altered in the TheWelcome and ThePortfolio
          // Don't forget the local folders and GitHub
          project.name === "1-SpotifyAPI" ||
          project.name === "3-RecordCollection" ||
          project.name === "5-FullStackToneRow" ||
          project.name === "2-RegionalWeather" ||
          project.name === "4-Joke-a-Quote-a-Day" ||
          project.name === "7-Portfolio" ||
          project.name === "6-DiceRollGames" ||
          project.name === "0-HomeInventoryApp" ||
          project.name === "0.5-QRCodeGenerator"
        );
      });
    });
  },
};
</script>



<style scoped>
h2 {
  padding-top: 20px;
}
.container {
  display: grid;
  gap: 20px;
  padding: 10px;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-auto-rows: 1fr;
}
.card {
  display: grid;
  grid-template-columns: 3fr 1fr;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  background-color: #5d475c;
  height: 100%;
}

.text-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 10px;
  color: white;
}

.button-link {
  display: flex;
  flex-direction: column;
  align-items: center;
}
a {
  color: white;
  text-decoration: none;
}
a:hover {
  color: #ee9b00;
}
.title {
  font-size: 16px;
  margin: 10px;
}

.image {
  flex: 2;
  display: flex;
  justify-content: center;
  flex-direction: column;
  padding: 20px;
}
img {
  width: 250px;
  height: 250px;
  border: solid 3px;
  border-color: #3d1f77;
}

@media (max-width: 590px) {
  .card {
    grid-template-columns: 1fr;
    grid-template-rows: auto auto;
  }
  .image {
    /* flex: 2; */
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    order: 1;
  }
}
h2 {
  text-align: center;
}
.repos {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  padding: 20px;
}
@media (max-width: 1000px) {
  .repos {
    grid-template-columns: 1fr;
  }
}
</style>