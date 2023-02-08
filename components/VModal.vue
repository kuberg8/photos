<template>
  <transition name="page">
    <div v-if="imageIndex || imageIndex == 0" class="modal">
      <transition-group name="fade">
        <img v-show="i === imageIndex" v-for="(item, i) in images" :key="i" :src="item" class="img" />
      </transition-group>

      <div @click="$emit('prev')" class="button prev">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="27" viewBox="0 0 16 27">
          <path
            stroke="none"
            d="M2815,1141.13l-13.86,12.86-2.13-2.13,11.78-10.93-11.79-11.8,2.13-2.13,13.86,13.86-0.13.14Z"
            transform="translate(-2799 -1127)"
          />
        </svg>
      </div>

      <div @click="$emit('next')" class="button next">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="27" viewBox="0 0 16 27">
          <path
            stroke="none"
            d="M2815,1141.13l-13.86,12.86-2.13-2.13,11.78-10.93-11.79-11.8,2.13-2.13,13.86,13.86-0.13.14Z"
            transform="translate(-2799 -1127)"
          />
        </svg>
      </div>

      <svg
        @click="$emit('close')"
        class="close"
        xmlns="http://www.w3.org/2000/svg"
        width="18"
        height="18"
        viewBox="0 0 18 18"
      >
        <path
          fill="none"
          fill-rule="evenodd"
          stroke="#000"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="1.5"
          d="M9 9.5l8-8-8 8-8-8 8 8zm0 0l8 8-8-8-8 8 8-8z"
        ></path>
      </svg>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      default: () => [],
    },
    imageIndex: Number,
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
