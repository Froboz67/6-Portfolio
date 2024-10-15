<template>
  <div>
    <h2>Projects</h2>
    <div class="repos">
      <div class="column" v-for="project in data" :key="project.id">
        <repo-component
          :title="project.name"
          :htmlUrl="project.html_url"
          :id="project.id"
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
      data: null,
    };
  },
  created() {
    githubService.getRepos().then((response) => {
      console.log(response);
      this.data = response.data.filter((project) => {
        return (
          project.name === "RecordCollection" ||
          project.name === "FullStackToneRow" ||
          project.name === "RegionalWeather"
        );
      });
    });
  },
};
</script>



<style scoped>
.repos {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  padding: 20px;
}
@media (max-width: 1000px) {
  .repos {
    grid-template-columns: 1fr;
  }
}
</style>