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
          project.name === "5-RandomToneRowGenerator" ||
          project.name === "2-RegionalWeather" ||
          project.name === "4-Joke-a-Quote-a-Day" ||
          project.name === "7-Portfolio" ||
          project.name === "6-DiceRollGames" ||
          project.name === "0-HomeInventoryApp" ||
          project.name === "0.5-QRCodeGenerator" ||
          project.name === "0.6-AudioToText"
        );
      });
    });
  },
};
</script>



<style scoped>
</style>