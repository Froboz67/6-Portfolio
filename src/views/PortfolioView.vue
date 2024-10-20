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
          project.name === "2-RecordCollection" ||
          project.name === "4-FullStackToneRow" ||
          project.name === "1-RegionalWeather" ||
          project.name === "3-Joke-a-Quote-a-Day" ||
          project.name === "6-Portfolio" ||
          project.name === "5-DiceRollGames"
        );
      });
    });
  },
};
</script>



<style scoped>
</style>