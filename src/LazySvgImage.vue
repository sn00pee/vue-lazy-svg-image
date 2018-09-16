<template>
  <div class='lazy-svg-image'>
    <component class="lazy-svg" :is="svg" ref="svg" :style="imageStyle" />
    <transition name="lazy-transition">
      <img class="lazy-image" :style="imageStyle" v-if="finished" :src="theImage.src" alt="">
    </transition>
  </div>
</template>

<script>

export default {
  name: "LazySvgImage",
  props: {
    svg: {
      type: Object,
      required: true
    },
    image:  {
      type: String,
      required: true
    },
    height: {
      type: [String, Number],
      default: 'auto'
    },
    width: {
      type: [String, Number],
      default: 300
    }
  },
  mounted() {
    this.$refs.svg.$el.addEventListener('animationend', () => {
      this.svgReady = true
    }, false)

    this.theImage = new Image()
    this.theImage.src = this.image
    this.theImage.onload = () => {
      this.isLoaded = true
    }
  },
  data: () => ({
    draw: null,
    theImage: null,
    svgReady: false,
    isLoaded: false
  }),
  computed: {
    finished() {
      return this.isLoaded && this.svgReady
    },
    imageStyle() {
      return {
        height: `${this.height}`,
        width: `${this.width}px`
      }
    }
  },
  watch: {
    finished(newv) {
      if (newv) {
        this.$emit('finished')
      }
    }
  },
}
</script>
<style lang="scss">
  .lazy-svg, .lazy-image {
    position: absolute;
  }
  .lazy-svg-image {

  }
  .lazy-transition {

  }

 .lazy-svg {
    path {
      stroke: #000;
      stroke-miterlimit: 10;
      stroke-width: 1px;
      fill: transparent;
      stroke-dasharray: 610;
      stroke-dashoffset: 610;
      // stroke-width: 0;
      animation: dash 600ms cubic-bezier(0.1, 0.37, 0.2, 0.6) forwards;
    }
  }

  @keyframes dash {
    to {
      stroke-dashoffset: 0;
    }
  }

  .lazy-image {
    z-index: 2;
    transition: opacity 300ms;
    &:hover {
      opacity: .1;
    }
  }

</style>
