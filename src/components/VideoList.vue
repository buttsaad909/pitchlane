<template>
  <div>
    <h2>Video Library</h2>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <ul>
        <li v-for="videoUrl in videos" :key="videoUrl">
          <p>Video: <a :href="videoUrl" target="_blank">{{ getFileNameFromUrl(videoUrl) }}</a></p>
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
        this.videos = response.data.videoUrls;
      } catch (error) {
        console.error('Error fetching videos:', error);
      } finally {
        this.loading = false;
      }
    },
    getFileNameFromUrl(url) {
      // Extract the filename from the URL (e.g., "1693840384074" from the original URL)
      const parts = url.split('/');
      return parts[parts.length - 1];
    },
  },
};
</script>
