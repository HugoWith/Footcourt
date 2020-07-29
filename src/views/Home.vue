<template>
  <div class="home">
    <header class="nav-header">
      <div class="logo">
        <router-link to="/">
          <h1 class="title">FOOTCOURT.</h1>
          <h3 class="title">All Highlights in one click</h3>
          <div class="underline-title"></div>
        </router-link>
      </div>
      <div class="input-search">
        <input type="text" v-model="searchQuery" placeholder="Search for a game" />
        <i class="fas fa-search"></i>
      </div>
    </header>
    <videoGallery :searchQuery="searchQuery" />
  </div>
</template>

<script>
// @ is an alias to /src
import videoGallery from "@/components/videoGallery.vue";

export default {
  name: "Home",
  components: { videoGallery },
  data() {
    return {
      searchQuery: ""
    };
  }
};
</script>

<style lang="scss">
body {
  font-family: "Lato", sans-serif;
}

a {
  text-decoration: none;
}

.title {
  position: relative;
  font-family: "Anton", sans-serif;
  color: black;
  z-index: 10;
}

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

.nav-header h1 h3 {
}

.nav-header {
  min-height: 10vh;
  font-size: 1rem;
  align-items: center;
  color: white;
  width: 90%;
  margin: auto;
  padding: 2rem 0rem;
  z-index: 2;
  position: relative;
  display: flex;
  justify-content: space-between;
}

.input-search input {
  width: 15rem;
  height: 2rem;
  border-radius: 1rem;
  padding: 10px;
  border: 2px solid black;
}

.input-search svg {
  color: black;
  font-size: 1rem;
  position: absolute;
  right: 1rem;
  margin-top: 6px;
}
</style>
