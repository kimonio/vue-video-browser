<template>
  <div class="container">
    <search-bar @term-change="onTermChange"></search-bar>
    <div class="row">
      <video-detail :video="selectedVideo"></video-detail>
      <video-list :videos="videos" @video-select="onVideoSelect"></video-list>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';
import VideoDetail from './components/VideoDetail.vue';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      videos: [],
      selectedVideo: null
    }
  },
  methods: {
    onTermChange(searchTerm) {
      axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: process.env.VUE_APP_YOUTUBE_API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      })
      .then(response => this.videos = response.data.items);
    },
    onVideoSelect(video) {
      this.selectedVideo = video;
    }
  }
}
</script>