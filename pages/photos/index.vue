
<template>
 
    <!-- directive -->
   
    <!-- component -->
    <viewer :images="images">
      <img v-for="src in images" :src="src.url" :key="src">
    </viewer>
  
</template>
<script>
import Vue from "vue";
import "viewerjs/dist/viewer.css";
import Viewer from "v-viewer";

Vue.use(Viewer); 
export default {
    data() { 
    return { 
        id:"",
        images: [] }
    },
     async fetch() { 
  this.id = this.$route.params.id;

      this.images = await fetch(
        'https://jsonplaceholder.typicode.com/albums/'+this.id+'/photos'
      ).then(res => res.json())
    },
  }
</script>
