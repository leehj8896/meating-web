<template>
  <input type="file" ref="image" @change="upload">
  <button v-on:click="submit"></button>
  <img id="uploaded-image" alt="Vue logo" v-bind:src="imageUploaded" v-if="imageUploaded">
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      imageUploaded: null,
    }
  },
  methods: {
    upload() {
      this.image = this.$refs.image.files[0]
      this.imageUploaded = URL.createObjectURL(this.image)
    },
    submit() {
      const baseUrl = 'localhost:8080'
      fetch(`${baseUrl}/image`, {
        method: 'POST',
        mode: 'no-cors',
        headers: { 
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(this.image)
      })
      .then(response => response.json())
      .then(data => (this.postId = data.id))
    }
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
#uploaded-image {
  width: 200px;
  height: 200px;
}
</style>
