<template>
  <div class="hello">
    <div class="container">
      <div class="gamesGallery">
        <div v-for="(video, index) in searchGame" :key="index">
          <router-link
            :to="{ name: 'highlightVideo', params: { id: video.title } }"
          >
            <p class="match-teams">{{ video.title }}</p>
            <p class="match-date">{{ video.date }}</p>

            <img :src="video.thumbnail" class="videoThumb" />
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "videoGallery",
  props: ["searchQuery"],

  data() {
    return {
      loading: false,
      videos: [],
      id: null,
      newDateFormat: null,
    };
  },
  methods: {
    fetchVideo() {
      this.loading = true;
      axios.get("https://www.scorebat.com/video-api/v1/").then((res) => {
        let allGames = res.data;
        allGames.forEach((game, index) => {
          let dateFormat = game.date;
          game.ind = index;
          this.getDate(dateFormat);
          game.date = this.newDateFormat;
          this.videos.push(game);
        });
        this.videos.forEach((i) => {
          this.id = i.title;
        });
      });
    },
    // addIndex() {

    //   console.log(this.videos);
    // },
    getDate(dateFormat) {
      const date = new Date(dateFormat);
      const dateTimeFormat = new Intl.DateTimeFormat("en", {
        year: "numeric",
        month: "short",
        day: "2-digit",
      });
      const [
        { value: month },
        ,
        { value: day },
        ,
        { value: year },
      ] = dateTimeFormat.formatToParts(date);

      // this.dates.push(`${day}-${month}-${year}`);

      this.newDateFormat = `${month}-${day}-${year}`;
    },
  },
  beforeMount() {
    this.fetchVideo();
  },
  computed: {
    searchGame() {
      // const searchInput = document.querySelector(".input-search input");
      // return searchInput.addEventListener("input", (e) => {
      //   this.searchQuery = e.target.value;
      return this.videos.filter((game) => {
        // console.log(game.title);
        // console.log(this.searchQuery);
        return game.title.toLowerCase().match(this.searchQuery.toLowerCase());
      });
      // });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
body {
  font-family: "Lato", sans-serif;
}

a {
  text-decoration: none;
  color: black;
}
.gamesGallery {
  display: grid;
  grid-gap: 20px;

  // grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-template-columns: 1fr 1fr 1fr;
  overflow: hidden;
  width: 100%;
}

.gamesGallery div {
  background: #f6f6f6;
  border-radius: 5px;
  min-height: 300px;
  text-align: center;
  padding: 15px;
  margin-bottom: 15px;
}

.container {
  width: 90vw;
  margin: 0 auto;
}

.videoThumb {
  width: 80%;
  border-radius: 5px;
  object-fit: cover;
  filter: contrast(120%);
}

.match-date {
  margin-bottom: 2rem;
}

.match-teams {
  font-weight: bold;
  font-size: 1.2rem;
}
</style>
