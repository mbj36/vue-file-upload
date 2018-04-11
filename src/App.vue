<template>
  <div id="app">
    <div v-if="!image">
      <h2>Select an image</h2>
      <input type="file" @change="onFileChange">
    </div>
    <div v-else>
      <img :src="image" />
      <button @click="removeImage">Remove image</button>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        image: ''
      }
    },
    methods: {
      removeImage() {
        this.image = ''
      },
      onFileChange(e) {
        const files = e.target.files || e.dataTransfer.files
        if (!files.length) return
        this.createImage(files[0])
      },
      createImage(file) {
        const image = new Image()
        const reader = new FileReader()
        const vm = this

        reader.onload = e => {
          vm.image = e.target.result
        }
        reader.readAsDataURL(file)
      }
    }
  }
</script>

<style scoped>
  img {
    width: 30%;
    margin: auto;
    display: block;
    margin-bottom: 10px;
  }
</style>
