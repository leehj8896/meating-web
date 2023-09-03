<template>
  <div id="container">
    <img id="logo" alt="Vue logo" src="./assets/logo.png">
    <div style="display: block"></div>
    <div class="filebox">
      <label for="file">사진 업로드</label>
      <input id="file" type="file" ref="image" @change="upload">
    </div>
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
  },
  methods: {
    upload() {
      this.image = this.$refs.image.files[0]
      this.imgSrc = URL.createObjectURL(this.image)
      this.imageUploaded = true
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
.filebox {
  margin-left: auto;
  margin-right: auto;
  margin-top: 50px;

  width: 280px;
  height: 80px;
  
  color: white;
  background-color: #f33;
}
.filebox label {
  display: block;
  color: #fff;
  
  line-height: 80px;    

  width: 100%;
  height: 100%;
}
.filebox input[type="file"] {
  display: none;
}
#beef-image {
  width: 280px;

  margin-top: 20px;

  background-color: grey;
}
#uploaded-image {
  width: 200px;
  height: 200px;
}
</style>
