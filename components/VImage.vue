<template>
  <div class="image">
    <nuxt-img v-if="loaded" :src="src" v-bind="$attrs" />
    <VLoder v-else />
  </div>
</template>

<script>
import VLoder from '~/components/VLoader.vue'

export default {
  components: {
    VLoder,
  },
  props: {
    src: { type: String, required: true },
  },
  data() {
    return { loaded: false }
  },
  mounted() {
    const img = new Image()
    img.src = this.src
    img.addEventListener('load', () => {
      this.loaded = true
    })
  },
}
</script>

<style lang="scss" scoped>
.image {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
