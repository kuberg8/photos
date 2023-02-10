<template>
  <nuxt-link class="card" :to="link" append>
    <div class="background" :style="{ backgroundImage: backgroundd }" />
    <div class="text">{{ title }}</div>
  </nuxt-link>
</template>

<script>
export default {
  props: {
    link: {
      type: String,
      default: '',
    },
    title: {
      type: String,
      default: '',
    },
    image: {
      type: String,
      default: '',
    },
    withGradient: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    backgroundd() {
      if (this.withGradient) {
        return `linear-gradient( rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4) ), url(${this.image})`
      }
      return `url(${this.image})`
    },
  },
}
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  color: #fff;

  .background {
    position: absolute;
    top: 0;
    left: 0;
    width: inherit;
    height: inherit;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    transition: transform 0.5s ease-out;
    z-index: 1;
  }

  .text {
    z-index: 2;
    text-transform: uppercase;
  }

  &:hover {
    .background {
      transform: scale(1.1);
    }
  }
}
</style>
