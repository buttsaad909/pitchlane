<template>
  <div>
    <h2>Upload Video</h2>
    <div class="custom-file">
      <input type="file" class="custom-file-input" id="customFile" @change="handleFileChange" accept="video/*">
      <button type="button" class="btn btn-primary" @click="uploadVideo">Upload</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  
  data() {
    return {
      selectedFile: null,
    };
  },
  methods: {
    handleFileChange(event) {
      this.selectedFile = event.target.files[0];
      console.log(this.selectedFile)
    },
    uploadVideo() {
      if (this.selectedFile) {
        const formData = new FormData();
        formData.append('video', this.selectedFile);
        axios.post('http://localhost:3000/api/upload', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
          },
        })
        .then(res => { 
          console.log(res)
        }).then(data => {
            // Retrieves video id from api reponse, passes it into Vue message for user. 
            let array = data.url.split("/");
            let id =  array[array.length-1];
            this.id = id
          })
        .catch(error => {
          console.log(error)
        });
      }
    },
  },
};
</script>