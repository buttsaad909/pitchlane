<template>
    <div>
      <h2>Video Library</h2>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <ul>
          <li v-for="video in videos" :key="video._id">
            {{ video.filename }}
          </li>
        </ul>
        <div v-if="videos.length === 0">No videos found.</div>
      </div>
    </div>
  </template>
  
  <script>
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
          const response = await fetch('https://rich-cyan-termite-hose.cyclic.app/api/retrieve');
          const data = await response.json();
          this.videos = data;
          console.log(this.videos)
          console.log(data)
        } catch (error) {
          console.error('Error fetching videos:', error);
        } finally {
          this.loading = false;
        }
      },
    },
  };
  </script>