<template>
  <div>
    <h2>Video Library</h2>
    <div v-if="loading">Loading...</div>
    <div v-else>
      <ul>
        <li v-for="videoUrl in videos" :key="videoUrl">
          <p>Video: <a :href="videoUrl" target="_blank">{{ videoUrl }}</a>
            <button @click="copyToClipboard(videoUrl)">Copy URL</button>
          </p>
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
        console.log(response.data); 
        this.videos = response.data.videoUrls; 
      } catch (error) {
        console.error('Error fetching videos:', error);
      } finally {
        this.loading = false;
      }
    },
    copyToClipboard(text) {
      const textarea = document.createElement('textarea');
      textarea.value = text;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);
      // You can optionally show a success message here
      console.log('URL copied to clipboard:', text);
    },
  },
};
</script>
