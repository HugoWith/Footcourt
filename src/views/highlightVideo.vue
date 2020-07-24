<template>
  <div class="hello">
    <h2>Games Gallery</h2>
    <div class="container">
      <p>coucou</p>
      <p>{{ id }}</p>
      <div v-html="highlight"></div>
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
