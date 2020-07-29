<template>
  <div class="hello">
    <header class="nav-header">
      <div class="logo">
        <router-link to="/">
          <h1 class="title">FOOTCOURT.</h1>
          <h3 class="title">All Highlights in one click</h3>
          <div class="underline-title"></div>
        </router-link>
      </div>
      <!-- <div class="input-search">
        <input type="text" v-model="searchQuery" placeholder="Search for a game" />
        <i class="fas fa-search"></i>
      </div>-->
    </header>
    <div class="container">
      <div class="match-teams-underline"></div>
      <div class="match-teams">
        <p>{{ id }}</p>
      </div>

      <div class="container-video-highlight">
        <div class="video-highlight">
          <div v-html="highlight"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "highlightVideo",
  props: ["id"],
  data() {
    return {
      highlight: null
    };
  },
  methods: {
    fetchVideo() {
      axios.get("https://www.scorebat.com/video-api/v1/").then(res => {
        let allGames = res.data;

        allGames.forEach(game => {
          if (game.title === this.id) {
            this.highlight = game.embed;
          }
        });
      });
    }
  },
  beforeMount() {
    this.fetchVideo();
  }
};
</script>

<style lang="scss">
.underline-title {
  width: 60%;
  height: 0.7rem;
  display: block;
  margin: 0 auto;
  background: #fffd6e;
  transform: translate(30px, -44px);
  z-index: 1;
  position: relative;
}

.video-highlight {
  width: 80%;
  margin: 0 auto;
}

.video-highlight iframe {
  border-radius: 1rem;
}

.container-video-highlight {
  width: 90%;
  background: #f6f6f6;
  border-radius: 1rem;
  margin: 0 auto;
  padding: 2rem;
}

.match-teams {
  position: relative;
  text-align: center;
  font-weight: bold;
  font-size: 1.5rem;
  margin-bottom: 20px;
  z-index: 10;
}

.match-teams-underline {
  width: 10%;
  height: 0.7rem;
  display: block;
  margin: 0 auto;
  background: rgb(255, 253, 110);
  transform: translate(60px, 30px);
  z-index: 1;
}
</style>