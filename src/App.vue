<template>
  <div>
    <search-bar @term-change="onTermChange"></search-bar>
    <video-list :videos="videos"></video-list>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return {
      videos: []
    }
  },
  methods: {
    onTermChange(searchTerm) {
      console.log("firing request");
      axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: process.env.VUE_APP_YOUTUBE_API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      })
      .then(response => this.videos = response.data.items);
    }
  }
}
</script>