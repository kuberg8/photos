<template>
  <div>
    <VIntro title="Lyuba & Marat" :image="back" />

    <div class="grid">
      <!-- TODO: добалять tall-panel в зависимости от размеров картинки -->
      <img
        v-for="(i, index) in 23"
        :key="index"
        :src="getRandomImage()"
        class="block"
        @click="imageIndex = index"
        :class="{ 'tall-panel': getRandomNum() == 2 }"
      />
    </div>

    <VModal
      :imageIndex="imageIndex"
      :images="['/example.jpeg', '/back.jpeg']"
      @next="imageIndex++"
      @prev="imageIndex--"
      @close="imageIndex = null"
    />
  </div>
</template>

<script>
import VIntro from '~/components/VIntro.vue'
import VModal from '~/components/VModal.vue'

import back from '~/static/back.jpeg'

export default {
  components: {
    VModal,
    VIntro
  },
  data() {
    return {
      back,
      imageIndex: null,
    }
  },
  mounted() {
    this.$root.setAnimation && this.$root.setAnimation()
  },
  methods: {
    getRandomNum() {
      return Math.floor(Math.random() * (2 - 1 + 1)) + 1
    },
    getRandomImage() {
      const num = this.getRandomNum()
      return num == 2 ? '/example.jpeg' : '/back.jpeg'
    },
  },
}
</script>

<style lang="scss" scoped>
.grid {
  display: grid;
  margin: 0 auto;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-auto-rows: minmax(50px, auto);
  padding: 50px;
  gap: 50px;

  .tall-panel {
    grid-row-end: span 2;
  }

  img {
    cursor: pointer;
  }
}
</style>
