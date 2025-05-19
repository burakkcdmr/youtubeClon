<template>
  <div class="container">
    <h1 class="title">Youtube Proje</h1>

    <SearchBar @term-change="onTermChange" />
    <div class="detailDiv">
      <VideoDetail :video="selectedVideo" />
      <VideoList @videoSelect="onVideoSelect" :videos="videos" />
    </div>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import VideoDetail from "./components/VideoDetail.vue";
import VideoList from "./components/VideoList.vue";

import axios from "axios";
export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data() {
    return {
      videos: [],
      selectedVideo: null,
    };
  },
  methods: {
    onTermChange(searchValue) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: "AIzaSyAPtGatoDfsVgXpWPFnW0COHe19L26Pt1E",
            type: "video",
            part: "snippet",
            q: searchValue,
          },
        })
        .then((response) => {
          this.videos = response.data.items;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    onVideoSelect(video) {
      this.selectedVideo = video;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.container {
  max-width: 1200px;
  width: 100%;
  margin: 50px auto;
}

.title {
  text-align: center;
}
.detailDiv {
  display: flex;
}
</style>
