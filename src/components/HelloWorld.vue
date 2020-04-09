<template>
  <div class="hello">
    <ul class="list-group list-group-flush">
    <li class="list-group-item flex-container" v-for="post in posts" :key="post.data.id" @click="openImage(post.data.preview.images[0].resolutions[1].url)">
        <img :src="post.data.thumbnail" alt="thumb" class="thumbnail">
        <span>{{ post.data.title }}</span>
    </li>
</ul>
  </div>
</template>

<script>
import axios from "axios"
import  {remote, ipcRenderer} from "electron"
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      posts: []
    }
  }
  ,
  created () {
    axios.get("https://reddit.com/r/aww.json")
      .then (response => {
        this.posts = response.data.data.children;
      })
      .catch(error => console.log(error));
  },
  methods: {
    openImage(image) {
      ipcRenderer.send("toggle-image", image)
      
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.flex-container {
  display: flex;
  align-items: center;
}
.thumbnail {
  width: 75px;
  height: 50px;
  border-radius: 15px;
  margin: 15px;
}

.list-group-item {
  cursor: pointer;
}

.list-group-item:hover {
  background-color: bisque;
}
</style>
