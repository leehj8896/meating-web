<template>
  <div style="font-size: 0.9rem; position: absolute; left: 1rem;">version {{ version }}</div>
  <div id="container">
    <img id="logo" alt="logo" src="./assets/logo-meating.png">
    <div class="filebox">
      <label for="file">사진 업로드</label>
      <input id="file" type="file" ref="image" @change="upload">
    </div>
    <div class="imagebox">
      <img id="beef-image" alt="소고기 이미지" v-bind:src="imgSrc">
      <div id="score">{{ scoreMessage }}</div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      imgSrc: require('./assets/question-mark2.png'),
      scoreMessage: '? 점',
      version: '1.0.2',
    }
  },
  methods: {
    upload() {
      this.image = this.$refs.image.files[0]
      if (!this.image) return
      this.imgSrc = URL.createObjectURL(this.image)

      try {
        const formData = new FormData()
        formData.append('file', this.image)
        console.log(`base url: ${process.env.VUE_APP_BASE_URL}`)
        this.scoreMessage = '계산중...'
        fetch(`${process.env.VUE_APP_BASE_URL}/grade`, {
          method: 'POST',
          body: formData
        })
        .then(response => {
          if (response.status === 200) return response.json()
          this.scoreMessage = '계산불가!'
        })
        .then(data => {
          console.log(JSON.stringify(data))
          this.score = `${data}`
        })  
      } catch (error) {
        console.log(JSON.stringify(error))
      }
    },
  }
}
</script>

<style>
html {
  height: 100%; 
  width: 100%;
  overflow: hidden;
  background-color: ivory;
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
  width: 50vw;
  height: 60vw;
}
.filebox {
  margin-left: auto;
  margin-right: auto;
  margin-top: 1vw;

  width: 75vw;
  height: 21vw;
  
  color: white;
  background-color: #f33;
  border-radius: 5px;
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
.imagebox {
  width: 75vw;
  height: 75vw;
  margin-top: 20px;
  background-color: grey;
  margin-left: auto;
  margin-right: auto;
}
#beef-image {
  width: 100%;
  height: 100%;
}
#score {
  margin-top: 1vw;
  font-size: larger;
}
</style>
