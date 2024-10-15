<template>
  <div class="container">
    <div class="card">
      <div class="text-content">
        <h2 class="title">
          <a :href="htmlUrl" target="_blank">{{ title }}</a>
        </h2>
        <p class="description">{{ description }}</p>
      </div>
      <div class="image">
        <img :src="getImage" alt="image" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      description: "",
    };
  },
  props: {
    title: String,
    htmlUrl: String,
    id: Number,
  },
  computed: {
    getImage() {
      return new URL(`../assets/images/${this.title}.png`, import.meta.url);
    },
  },
  created() {
    this.fetchDescription();
  },
  methods: {
    fetchDescription() {
      const url = new URL(`../assets/text/${this.title}.txt`, import.meta.url);
      fetch(url)
        .then((response) => response.text())
        .then((data) => {
          console.log(data);
          this.description = data;
        })
        .catch((error) => {
          console.log.error("problem fetching description", error);
        });
    },
  },
};
</script>

<style scoped>
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
  background-color: #94d2bd;
  height: 100%;
}

.text-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 10px;
}

a {
  color: white;
  text-decoration: none;
}
a:hover {
  color: #ee9b00;
}
.title {
  text-align: left;
  font-size: 20px;
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
  width: 150px;
  height: 150px;
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
</style>