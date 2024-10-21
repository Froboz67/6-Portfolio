<template>
  <div class="container">
    <div class="card" :class="{ reverse: isReverse }">
      <div class="text-content">
        <h4 class="title">
          <button class="title-button">
            <a :href="htmlUrl" target="_blank" class="button-link">
              <span>{{ title.slice(2) }}</span>
              <span>GitHub</span>
            </a>
          </button>
        </h4>
        <p class="description">{{ description }}</p>
      </div>
      <div class="image">
        <img :src="getImage" :alt="`${title} project screenshot`" />
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
    index: Number,
  },
  computed: {
    getImage() {
      return new URL(`../assets/images/${this.title}.png`, import.meta.url);
    },
    isReverse() {
      return this.index % 2 !== 0;
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
  background-color: #3d1f77;
  height: 100%;
}
.reverse {
  grid-template-columns: 1fr 3fr;
}
.reverse .text-content {
  order: 2;
}
.text-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 10px;
  color: white;
  order: 1;
}
.title-button {
  background-color: #5d475c;
  border-radius: 10px;
  padding: 5px 15px 5px 15px;
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
  color: #2f135d;
}
.title {
  font-size: 16px;
  margin: 10px;
  display: flex;
  justify-content: flex-start;
}
.reverse .title {
  justify-content: flex-end;
}
.image {
  flex: 2;
  display: flex;
  justify-content: center;
  flex-direction: column;
  padding: 20px;
  order: 2;
}
.reverse .image {
  order: 1;
}
img {
  width: 250px;
  height: 250px;
  border: solid 3px;
  border-color: #3d1f77;
  border-radius: 7px;
}

@media (max-width: 590px) {
  .card {
    grid-template-columns: 1fr;
    grid-template-rows: auto auto;
    justify-items: center;
  }
  .image {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    order: 2;
  }
  .text-content {
    order: 3;
  }
  .title {
    order: 1;
    justify-content: center;
  }
  .reverse .title {
    order: 1;
    justify-content: center;
  }
}
</style>