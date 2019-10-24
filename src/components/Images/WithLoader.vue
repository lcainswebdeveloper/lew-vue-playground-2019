<template>
    <div class="relative img-loader-container" :style="containerStyles">
        <div class="image-loader" v-if="!ready"></div>
        <img @load="imgLoaded" :src="imgSrc" class="loaded-image" :class="{'is-loaded':ready == true}">
    </div>
</template>

<script>
export default {
  props: {
    imgSrc: { required: true },
    imgWidth: { default: 500 },
    imgHeight: { default: 500 },
  },
  computed: {
    requiredTopPadding() {
      return (this.imgHeight / this.imgWidth) * 100;
    },
    containerStyles() {
      return {
        width: '100%',
        'max-width': `${this.imgWidth}px`,
        'padding-top': `${this.requiredTopPadding}%`,
      };
    },
  },
  methods: {
    imgLoaded() {
      setTimeout(() => {
        this.ready = true;
      }, 1000);
    },
  },
  data() {
    return {
      ready: false,
    };
  },
};
</script>

<style lang="scss">
    .relative{
        position: relative;
    }
    .full_width{
        width:100%;
    }
    .img-loader-container{
        background:#f3f3f3;
        .loaded-image{
            max-width:100%;
            position:absolute;
            top:0px;
            left:0px;
            opacity:0;
            transition:all 0.3s ease;
        }
        .loaded-image.is-loaded{
            opacity:1;
        }
    }
    .image-loader {
        display: inline-block;
        width:46px;
        height:46px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
    }
    .image-loader:after {
        content: " ";
        display: block;
        width: 46px;
        height: 46px;
        margin: 1px;
        border-radius: 50%;
        border: 5px solid #fff;
        border-color: #fff transparent #fff transparent;
        animation: spin-load 1.2s linear infinite;
    }
    @keyframes spin-load {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg);
        }
    }
</style>
