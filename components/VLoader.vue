<template>
  <svg :style="{ width, height }" class="circular-loader" width="100%" height="100%" viewBox="0 0 42 42">
    <circle cx="21" cy="21" r="13.6" fill="#ffffff" stroke-width="0.2"></circle>
    <circle
      class="loader-path"
      cx="21"
      cy="21"
      r="15.91549430918954"
      fill="transparent"
      stroke="currentColor"
      stroke-width="4.5"
    ></circle>
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: String,
      default: '80px',
    },
    height: {
      type: String,
      default: '80px',
    },
  },
}
</script>

<style lang="scss" scoped>
.circular-loader {
  -webkit-animation: rotate 2s linear infinite;
  animation: rotate 2s linear infinite;
  -webkit-transform-origin: center center;
  -ms-transform-origin: center center;
  transform-origin: center center;
  margin: auto;
}

.loader-path {
  stroke-dasharray: 150, 200;
  stroke-dashoffset: -10;
  -webkit-animation: dash 1.2s ease-in-out infinite;
  animation: dash 1.2s ease-in-out infinite;
  stroke-linecap: round;
}

@-webkit-keyframes rotate {
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}

@keyframes rotate {
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
@-webkit-keyframes dash {
  0% {
    stroke-dasharray: 1, 200;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -20;
  }
  100% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -94;
  }
}
@keyframes dash {
  0% {
    stroke-dasharray: 1, 200;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -20;
  }
  100% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -94;
  }
}
</style>
