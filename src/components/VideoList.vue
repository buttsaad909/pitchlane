<template>
  <div>
    <h2>Video Library</h2>
    {{ videos }}
    <div v-if="loading">Loading...</div>
    <div v-else>
      <ul>
        <li v-for="videoUrl in videos" :key="videoUrl">
          <a :href="videoUrl" target="_blank">{{ videoUrl }}</a>
          <p>videoUrl</p>
        </li>
      </ul>
      <div v-if="videos.length === 0">No videos found.</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      videos: [],
      loading: true,
    };
  },
  mounted() {
    this.fetchVideos();
  },
  methods: {
    async fetchVideos() {
      try {
        const response = await axios.get('https://rich-cyan-termite-hose.cyclic.app/api/retrieve');
        const data = await response.json();
        this.videos = data.videoUrls;
        console.log(this.videos);
      } catch (error) {
        console.error('Error fetching videos:', error);
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>
