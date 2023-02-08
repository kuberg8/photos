<template>
  <div
    class="intro"
    :style="{ backgroundImage: `linear-gradient( rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.3) ), url(${image})`, alignItems }"
  >
    <slot>
      <h1 class="title">{{ title }}</h1>
    </slot>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: '',
    },
    image: {
      type: String,
      default: '',
    },
    alignItems: {
      type: String,
      default: 'flex-end',
    },
  },
}
</script>

<style lang="scss" scoped>
.intro {
  position: relative;
  display: flex;
  text-align: center;
  justify-content: center;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  width: 100%;
  min-height: 100vh;
  padding: 80px;
  color: white;

  .title {
    animation: translateY 1s;
  }

  a {
    transition: opacity 0.2s;
    &:hover {
      color: #fff;
      opacity: 0.8;
    }
  }
}
</style>
