<template>
import func from './vue-temp/vue-editor-bridge';
  <div class="imagic">
    <div class="imagic-image" :class="{ 'blur': pseudoBlur }" :style="imagicStyleLoad()" >
    </div>
    <div class="imagic-loader-wrapper" :style="loadWrapperStyle" v-if="!imageLoaded">
      <h3 style="title" v-if="src === null">{{ errorTitle }}</h3>
      <!-- <h3 style="title" >{{ imagicStyle }}</h3> -->
      <div class="loader" v-if="src !== null"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'imagic',
  props: {
    src: {
      default: null,
      required: false
    },
    src_big: {
      default: null,
      required: false
    },
    blur: {
      default: false,
      required: false
    },
    width: {
      default: '100%',
      required: false
    },
    height: {
      default: '100%',
      required: false
    },
    square: {
      default: true,
      required: false
    },
    loadWrapper: {
      default: '#e5e5e5',
      required: false
    },
    errorTitle: {
      default: 'Sorry, image did not load.',
      required: false
    }
  },
  data () {
    return {
      imageLoaded: false,
      imagicImage: {
        width: (this.square) ? '100%' : this.width,
        paddingTop: (this.square) ? '100%' : this.height,
        backgroundImage: null
      },
      pseudoBlur: true,
      loadWrapperStyle: {
        backgroundColor: this.loadWrapper
      }
    }
  },
  methods: {
    imagicStyleLoad () {
      // let image = new Image()
      // image.onload = () => {
      //   // console.log('LOADED')
      //   this.imageLoaded = true
      //   this.imagicImage.backgroundImage = 'url("' + this.src + '")'
      //   if (this.blur === false) {
      //     if (this.src_big === null) {
      //       setTimeout(() => {
      //         this.pseudoBlur = false
      //       }, 300)  
      //     } else {
            
      //     }
      //   }
      // }
      // image.src = this.src
      this.loadImage(this.src).then(res => {
        console.log(res)
      })
      return this.imagicImage
    },
    async loadImage(url) {
      let image = new Image()
      let result_url = null
      image.onload = await function() {
        result_url = 'url("' + this.src + '")'
      }
      image.src = url
      return result_url
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.imagic{
  overflow: hidden;
  position: relative;
  width: 100%;
}
.imagic-image{
  width: 100%;
  padding-top: 100%;
  background-color: #e5e5e5;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  transition: transform .3s ease-in-out;
}
.imagic-image.blur{
  filter: blur(10px);
  transform: scale(1.5);
}
.title {
  text-align: center;
  width: 100%;
}
.imagic-loader-wrapper{
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
.loader {
  border: 5px solid rgba(0, 0, 0, 0.05);
  border-radius: 50%;
  border-top: 5px solid rgba(0, 0, 0, 0.15);
  width: 30px;
  height: 30px;
  -webkit-animation: spin 1s linear infinite; /* Safari */
  animation: spin 1s linear infinite;
}

/* Safari */
@-webkit-keyframes spin {
  0% { -webkit-transform: rotate(0deg); }
  100% { -webkit-transform: rotate(360deg); }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
