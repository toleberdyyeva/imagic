<template>
  <div>
      <h1>Simple Image Async Loading </h1>
      <div style="width:100px; height: 1000px;">
        <imagic height='100%' :src='image.big' v-model="image.laoded" :loader='false'  />
        {{ image.laoded }}
      </div>
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
      images: [
        {
          sm: 'https://res.cloudinary.com/demo/image/upload/waa_70,h_53,c_scale/turtles.jpg',
          big: 'https://res.cloudinary.com/demo/image/upload/turtles.jpg',
          laoded: false,
        },
      ],
      image: {
          sm: 'https://res.cloudinary.com/demo/image/upload/waa_70,h_53,c_scale/turtles.jpg',
          big: 'https://res.cloudinary.com/demo/image/upload/turtles.jpg',
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
