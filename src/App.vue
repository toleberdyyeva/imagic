<template>
  <div>
    <div style="width:50%">
      <h1>Simple Image Async Loading </h1>
      <div v-for="(image, index) in images" :key="index" >
        <imagic height='300px;' :src='image.big' />
        {{ image }}
        <br>
      </div>
    </div>
  </div>
</template>
<script>
import Imagic from './components/Imagic'
export default {
  name: 'App',
  data () {
    return {
      images: [
        {
          sm: 'https://res.cloudinary.com/demo/image/upload/w_70,h_53,c_scale/turtles.jpg',
          big: 'https://res.cloudinary.com/demo/image/upload/turtles.jpg',
          laoded: false,
        },
        // {
        //   sm: 'https://www.goo.ne.jp/green/column/upload/img/thumbnail/authorsbeauty/wp-content/uploads/2016/06/215a018de5f08bc60f9608a158b011d6.jpg',
        //   big: 'https://www.goo.ne.jp/green/column/upload/img/thumbnail/authorsbeauty/wp-content/uploads/2016/06/215a018de5f08bc60f9608a158b011d6.jpg',
        //   laoded: false,
        // },
        // {
        //   sm: 'https://i.amz.mshcdn.com/niKEQtUKLRjVeprnNwCfQGnBc78=/950x534/filters:quality(90)/https%3A%2F%2Fblueprint-api-production.s3.amazonaws.com%2Fuploads%2Fcard%2Fimage%2F511986%2F56fe7642-b053-4667-89dc-e2d3abea5333.jpg',
        //   big: 'https://i.amz.mshcdn.com/niKEQtUKLRjVeprnNwCfQGnBc78=/950x534/filters:quality(90)/https%3A%2F%2Fblueprint-api-production.s3.amazonaws.com%2Fuploads%2Fcard%2Fimage%2F511986%2F56fe7642-b053-4667-89dc-e2d3abea5333.jpg',
        //   laoded: false,
        // }
      ]
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
