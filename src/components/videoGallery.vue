<template>
  <div class="hello">
    <h2>Games Gallery</h2>
    <div class="container">
      <div class="gamesGallery">
        <div v-for="(video, index) in videos" :key="index">
          <router-link :to="{ name: 'highlightVideo', params: { id: video.title } }">
            <p>{{ video.title }}</p>
            <p>{{video.date}}</p>

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

  data() {
    return {
      loading: false,
      videos: [],
      id: null
    };
  },
  methods: {
    fetchVideo() {
      this.loading = true;
      axios.get("https://www.scorebat.com/video-api/v1/").then(res => {
        let allGames = res.data;
        allGames.forEach((game, index) => {
          let dateFormat = game.date;
          game.ind = index;
          this.getDate(dateFormat);
          this.videos.push(game);
        });
        this.videos.forEach(i => {
          this.id = i.title;
          console.log(this.id);
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
        day: "2-digit"
      });
      const [
        { value: month },
        ,
        { value: day },
        ,
        { value: year }
      ] = dateTimeFormat.formatToParts(date);

      // this.dates.push(`${day}-${month}-${year}`);
      return day, month, year;

      // console.log(`${day}-${month}-${year}`);
    }
  },
  beforeMount() {
    this.fetchVideo();
  },
  computed() {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
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
}

.container {
  width: 95vw;
  margin: 0 auto;
}

.videoThumb {
  width: 50%;
}
</style>
