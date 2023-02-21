<template>
  <!-- TODO: Предусмотреть отрытие альбома без родителя(списка папок) -->
  <div л>
    <VIntro v-if="cover" :title="cover.customMetadata.albom" :image="cover.url" />

    <div class="grid">
      <img
        v-for="(image, index) in photos"
        :key="index"
        :src="image.url"
        class="block"
        :class="{ 'tall-panel': image.height > image.width }"
        @click="imageIndex = index"
        @load="load"
      />
      <!-- loading="lazy" -->
      <!-- format="webp" -->
      <!-- quality="10" -->
    </div>

    <VModal
      v-if="typeof imageIndex === 'number'"
      :imageIndex="imageIndex"
      :images="photosUrl"
      @next="imageIndex < photosUrl.length - 1 && imageIndex++"
      @prev="imageIndex > 0 && imageIndex--"
      @close="imageIndex = null"
    />
  </div>
</template>

<script>
import VIntro from '~/components/VIntro.vue'
import VModal from '~/components/VModal.vue'

export default {
  components: {
    VModal,
    VIntro,
  },
  data() {
    return {
      imageIndex: null,
      photos: [],
      cover: null,
      pageName: '',
    }
  },
  mounted() {
    this.pageName = this.$route?.params?.id?.replaceAll('_', ' ')
    this.$axios.$get(`/files?format=webp&path=${decodeURIComponent(this.$route.path)}`).then(([cover, ...photos]) => {
      this.cover = cover
      this.photos = photos
    })
  },
  computed: {
    photosUrl() {
      return this.photos.map(({ url }) => url)
    },
  },
  head() {
    return {
      title: `Альбом | ${this.pageName}`,
    }
  },
  methods: {
    load({ target }) {
      this.$root.setAnimation(target)
    },
  },
}
</script>

<style lang="scss" scoped>
.grid {
  display: grid;
  margin: 0 auto;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-auto-rows: minmax(50px, auto);
  padding: 50px;
  gap: 50px;

  .tall-panel {
    grid-row-end: span 2;
  }

  img {
    cursor: pointer;
    // background: grey;
  }
}
</style>
