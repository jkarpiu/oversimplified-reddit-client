<template>
  <div class="about">
    <img :src="imageUrl" alt="image">
  </div>
</template>

<script>
import { ipcRenderer } from 'electron'
export default {
  created() {
    ipcRenderer.on('image', (event, arg) => {
      console.log(arg)
      this.imageUrl = arg
    })
  },
  data() {
    return {
      imageUrl: ''
    }
  }
}
</script>
