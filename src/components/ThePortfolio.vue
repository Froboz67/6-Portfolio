<template>
  <div class="container">
    <div class="card" :class="{ reverse: isReverse }">
      <div class="text-content">
        <h4 class="title">
          <button class="title-button">
            <a :href="htmlUrl" target="_blank" class="button-link">
              <span v-if="title[1] === '.'">{{ title.slice(4) }}</span>
              <span v-else>{{ title.slice(2) }}</span>
              <span>GitHub</span>
            </a>
          </button>
          <button
            v-if="videoCheckCompleted && videoExists"
            class="title-button"
            @click="playVideo"
          >
            <a target="" class="button-link">
              <span>Play Video</span>
            </a>
          </button>
          <button v-if="appExists" class="title-button">
            <a :href="appUrl" target="_blank" rel="noopener noreferrer">
              <span>Try App</span>
            </a>
          </button>
        </h4>
        <p class="description">{{ description }}</p>
      </div>
      <div class="image">
        <img :src="getImage" :alt="`${title} project screenshot`" />
      </div>
    </div>
    <div v-if="showVideo" class="modal">
      <div class="modal-content">
        <span class="close-button" @click="closeVideo">&times;</span>
        <video controls autoplay>
          <source :src="videoUrl" type="video/mp4" />
          Your browser does not support the video tag.
        </video>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      description: "",
      showVideo: false,
      videoExists: false,
      videoCheckCompleted: false,
      appExists: false,
      appCheckCompleted: false,
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
    videoUrl() {
      const url = new URL(`../assets/images/${this.title}.mp4`, import.meta.url)
        .href;
      return url;
    },
  },
  created() {
    // makes sure all the data is loaded before the DOM is created
    this.fetchDescription();
    this.checkVideoExists();
    this.checkAppExists();
  },
  methods: {
    playVideo() {
      this.showVideo = true;
    },
    closeVideo() {
      this.showVideo = false;
    },
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
    checkVideoExists() {
      // hard coded array for video files
      const availableVideos = [
        "1-SpotifyAPI.mp4",
        "0-HomeInventoryApp.mp4",
        "0.5-QRCodeGenerator.mp4",
      ]; // Add all existing video file names here DON'T FORGET THE COMMA!!!!
      this.videoExists = availableVideos.includes(`${this.title}.mp4`);
      this.videoCheckCompleted = true;
    },
    checkAppExists() {
      // hard coded array for deployed apps
      const availableApps = [
        "https://2-regionalweather.netlify.app/",
        "https://4-joke-a-quote-a-day.netlify.app/",
        "https://5-randomtonerowgenerator.netlify.app/",
      ];
      const titleLower = this.title.toLowerCase();
      this.appExists = availableApps.includes(
        `https://${titleLower}.netlify.app/`
      );
      if (this.appExists) {
        this.appUrl = `https://${titleLower}.netlify.app/`;
      }
      this.appCheckCompleted = true;
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1001;
}

.modal-content video {
  width: 100%; /* Make video take full modal-content width */
  /* height: auto;  */
  max-height: 100%;
  object-fit: contain;
  border-radius: 10px;
}

.modal-content {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 80%;
  max-height: 80%;
  border-radius: 10px;
  /* overflow: hidden; */
}
.close-button {
  position: absolute;
  top: 1rem;
  right: 1.5rem;
  font-size: 3rem;
  color: red;
  cursor: pointer;
  background: solid red;
  border: 1px solid red;
  outline: none;
  z-index: 1030;
}

.close-button:hover {
  color: #ccc; /* Change color on hover */
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
  padding: 0.3rem 1rem 0.3rem 1rem;
  margin: 0.5rem;
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

@media (max-width: 800px) {
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
@media (max-width: 480px) {
  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .text-content,
  .image {
    width: 100%;
    text-align: center;
  }
}
</style>