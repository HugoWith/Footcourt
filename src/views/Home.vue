<template>
  <div class="home">
    <h1>Foot Court</h1>
    <videoGallery />
  </div>
</template>

<script>
// @ is an alias to /src
import videoGallery from "@/components/videoGallery.vue";

export default {
  name: "Home",
  components: { videoGallery }
};
</script>
