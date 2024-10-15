
<template>
  <!-- <h1>Home Page</h1> -->
  <!-- <h2>My name is Kevin and I am a developer</h2> -->
  <div class="bio">
    <p class="bio-text">{{ bio }}</p>
  </div>
</template>


<script>
export default {
  data() {
    return {
      bio: "",
    };
  },
  created() {
    this.fetchBio();
  },
  methods: {
    fetchBio() {
      const url = new URL(`../assets/text/AboutHome.txt`, import.meta.url);
      fetch(url)
        .then((response) => response.text())
        .then((data) => {
          console.log(data);
          this.bio = data;
        })
        .catch((error) => {
          console.log.error("problem fetching bio", error);
        });
    },
  },
};
</script>

<style scoped>
.bio-text {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 50vw;
  padding: 25px;
  place-items: center;
  margin: 0 auto;
  margin-top: 50px;
  background-color: #94d2bd;
  border-radius: 5px;
}
</style>

