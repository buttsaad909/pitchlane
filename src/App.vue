<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <VideoUpload msg="Welcome to Your Vue.js App"/>
  <VideoList />
</template>

<script>
import VideoUpload from './components/VideoUpload.vue'
import VideoList from './components/VideoList.vue';
//import VideoFile from './components/VideoFile.vue'

export default {
  name: 'App',
  components: {
    VideoUpload,
    VideoList,
    //VideoFile,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
