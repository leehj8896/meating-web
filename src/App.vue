<template>
  <div id="container">
    <img id="logo" alt="Vue logo" src="./assets/logo.png">
    <div style="display: block"></div>
    <button id="upload-button" >사진 업로드</button>
    <img id="beef-image" alt="소고기 이미지" v-bind:src="imgSrc" v-if="!imageUploaded">
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      imageUploaded: false,
      imgSrc: require('./assets/question-mark2.png')
    }
  }
}
</script>

<style>
html {
  height: 100%; 
  width: 100%;
  overflow: hidden;
}
#container {
  width: 100%;
  text-align: center;
  margin: 0; 
  padding: 0;
}
#logo {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
#upload-button {
  all: unset;
  display: block;

  margin-left: auto;
  margin-right: auto;
  margin-top: 50px;

  width: 280px;
  height: 80px;
  
  color: white;
  background-color: #f33;
}
#beef-image {
  width: 280px;

  margin-top: 20px;

  background-color: grey;
}
</style>
