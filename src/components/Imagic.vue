<template>
  <div class="imagic">
    <div class="imagic-image" :class="{ 'blur': pseudoBlur }" :style="imagicStyleLoad()" >
    </div>
    <div class="imagic-loader-wrapper" :style="loadWrapperStyle" v-if="!imageLoaded">
      <h3 style="title" v-if="imageError">{{ errorTitle }}</h3>
      <!-- <h3 style="title" >{{ imagicStyle }}</h3> -->
      <div class="loader" v-if="!imageLoaded"></div>
    </div>
  </div>
</template>
<script>
/* eslint-disable */
// TODO:  Make Event handle for Image loaded status 
//           Also prepare a beatifull README.md :D 
// FIXME: add time delay for blur-out

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
      default: null,
      required: false
    },
    height: {
      default: null,
      required: false
    },
    loadWrapperColor: {
      default: '#e5e5e5',
      required: false
    },
    errorTitle: {
      default: 'Sorry, image did not load.',
      required: false
    },
    afterDelay: {
      default: 1000,
      required: false,
    }
  },
  data () {
    return {
      imageLoaded: false,
      imageError: false,
      imagicImage: {
        'padding-top' : (this.height === null) ? '100%' : this.height  ,
        backgroundImage: null
      },
      pseudoBlur: true,
      loadWrapperStyle: {
        backgroundColor: this.loadWrapperColor
      },
      startLoading: false,
    }
  },
  methods: {
    imagicStyleLoad () {
      if (this.src !== null && !this.startLoading) {
        this.startLoading = true
        this.loadImage(this.src).then(res => { //  Start loading a normal image 
          this.imagicImage.backgroundImage = res  // Setting a default source image 
          this.imageLoaded = true // open normal image and stay blurring it 
          this.loadImage(this.src_big).then(Response => { // loading Big image 
            this.imagicImage.backgroundImage = Response // setting new Big image
            setTimeout(() => {
              this.finishLoaded(true) // open from blurring  with big image  
            },this.afterDelay)
          }).catch(err => { // if Big Image loading failed 
            setTimeout(() => {
              this.finishLoaded(true) // open from blurring  with small image 
            },this.afterDelay)
          })
        }).catch(err => {
          this.imageError =  true
          this.finishLoaded(false)
        })
      }
      return this.imagicImage
    },
    finishLoaded(status){
      if (status) { this.pseudoBlur = (this.blur) ? true : false }
      else { this.pseudoBlur = status  }
      this.$emit('input', status) 
    },
    loadImage(url) {
      return new Promise((resolve, reject ) => {
        let image = new Image()
        let result_url = null
        image.onload = () =>  {
          result_url = 'url("' + url + '")'
          resolve(result_url)
        }
        image.onerror = () => {
          reject(null)
        }
        image.src = url
      })  
    }
  },
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
  background-color: #e5e5e5;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  transition: transform .3s ease-in-out;
  -webkit-transition: -webkit-transform .3s ease-in-out;
  transition: -webkit-transform .3s ease-in-out;
  transition: transform .3s ease-in-out;
}
.imagic-image.blur{
  filter: blur(20px);
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

