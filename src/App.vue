<template>
  <div>
      <h1>Simple Image Async Loading </h1>
      <input type="text" v-model="imageLink">
      <div style="width: 300px; height: 300px;">
        <imagic height='100%' :src='image.big' :src_big="imageLink" v-model="image.laoded" :loader='false'  />
        {{ image.laoded }}
      </div>
    </div>
</template>
<script>
/* eslint-disable */
import Imagic from './components/Imagic'
export default {
  name: 'App',
  data () {
    return {
      imageLink: 'https://res.cloudinary.com/demo/image/upload/turtles.jpg',
      images: [
        {
          sm: 'https://res.cloudinary.com/demo/image/upload/waa_70,h_53,c_scale/turtles.jpg',
          big: 'http://test.foxout.kz/media/events_core/posters/asd.png',
          laoded: false,
        },
      ],
      image: {
          sm: 'https://res.cloudinary.com/demo/image/upload/waa_70,h_53,c_scale/turtles.jpg',
          big: 'http://test.foxout.kz/media/events_core/posters/asd.png',
          laoded: false,
      },
    }
  },
  components: {
    Imagic
  }
}
</script>

<style>
  *{
    font-family: Arial, Helvetica, sans-serif;
  }
</style>
