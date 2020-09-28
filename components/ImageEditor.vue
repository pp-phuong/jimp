<template>
  <div id="image-editor">
    <div>
      <!-- upload img -->
      <div v-if="!image">
        <h3>Select an image</h3>
        <input type="file" @change="onFileChange" />
      </div>
      <!-- change img -->
      <div v-else>
        <img :src="image" />
        <button @click="removeImage">Change image</button>
        <!-- chỉnh sửa hình ảnh -->
        <div>
          <button @click="onRotate">Xoay ảnh</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// import Jimp from 'jimp'
export default {
  data() {
    return {
      image: '',
    }
  },
  methods: {
    onFileChange(e) {
      const files = e.target.files || e.dataTransfer.files
      if (!files.length) return
      this.createImage(files[0])
    },
    createImage(file) {
      this.image = new Image()
      const reader = new FileReader()
      const vm = this

      reader.onload = (e) => {
        vm.image = e.target.result
      }
      reader.readAsDataURL(file)
    },
    removeImage(e) {
      this.image = ''
    },
    onRotate() {
      // const image = Jimp.read(this.image)
      // image.flip(true, false)
    },
  },
}
</script>
<style scoped>
#image-editor {
  text-align: center;
}
img {
  width: 30%;
  margin: auto;
  display: block;
  margin-bottom: 10px;
}
</style>
