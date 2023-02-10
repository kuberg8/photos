<template>
  <transition name="page">
    <div v-if="imageIndex || imageIndex == 0" class="modal">
      <transition-group name="fade">
        <nuxt-img
          v-show="item === images[imageIndex]"
          v-for="(item, i) in trimImages"
          :key="i"
          :src="item"
          quality="10"
          format="webp"
          class="img"
        />
      </transition-group>

      <div v-if="!isFirstImage" @click="prevImg" class="button prev">
        <img :src="svgArrow" class="svg" />
      </div>

      <div v-if="!isLastImage" @click="nextImg" class="button next">
        <img :src="svgArrow" class="svg" />
      </div>

      <img :src="svgClose" @click="$emit('close')" class="close svg" />
    </div>
  </transition>
</template>

<script>
import svgClose from '~/static/images/svg/close.svg'
import svgArrow from '~/static/images/svg/arrow.svg'

export default {
  props: {
    images: {
      type: Array,
      default: () => [],
    },
    imageIndex: {
      type: Number,
      default: null,
      require: true,
    },
  },
  data() {
    const leftNumber = this.imageIndex === 0 ? 0 : this.imageIndex - 1
    const rightNumber = this.imageIndex === this.images.length - 1 ? this.images.length : this.imageIndex + 1

    return {
      leftNumber,
      rightNumber,
      svgClose,
      svgArrow,
    }
  },
  methods: {
    prevImg() {
      this.$emit('prev')
      this.leftNumber > 0 && this.rightNumber--
    },
    nextImg() {
      this.$emit('next')
      this.rightNumber < this.images.length - 1 && this.rightNumber++
    },
  },
  computed: {
    isFirstImage() {
      return this.imageIndex === 0
    },
    isLastImage() {
      return this.imageIndex === this.images.length - 1
    },
    trimImages() {
      return this.images.slice(this.leftNumber, this.rightNumber + 1)
    },
  },
}
</script>

<style lang="scss" scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: #fff;
  z-index: 100;

  .svg {
    width: 25px;
    height: 25px;
    object-fit: contain;
  }

  .img {
    max-height: 90vh;
    max-width: 60vw;
    object-fit: contain;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
  }

  .close {
    position: fixed;
    right: 5vh;
    top: 5vh;
    cursor: pointer;
    z-index: 102;
  }

  .button {
    position: fixed;
    z-index: 101;
    top: 0;
    height: 100vh;
    width: 10vw;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  .next {
    right: 0;
  }

  .prev {
    left: 0;
    transform: rotate(180deg);
  }
}
</style>
