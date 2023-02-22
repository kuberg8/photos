<template>
  <!-- TODO: Предусмотреть отрытие альбома без родителя(списка папок) -->
  <div>
    <VIntro v-if="cover" :title="cover.customMetadata.albom" :image="cover.url" class="banner" />

    <div v-if="imgLoaded" class="grid">
      <div
        v-for="(image, index) in photos"
        :key="index"
        :class="{ 'tall-panel': image.height > image.width }"
        :style="{ background: getRandomColor() }"
      >
        <nuxt-img
          :src="image.url"
          loading="lazy"
          format="webp"
          quality="10"
          @click="imageIndex = index"
          @load="load"
        />
      </div>
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
      imgLoaded: false,
    }
  },
  mounted() {
    this.pageName = this.$route?.params?.id?.replaceAll('_', ' ')
    this.$axios
      .$get(`/files?format=webp&path=${decodeURIComponent(this.$route.path)}`)
      .then(([cover, ...photos]) => {
        this.cover = cover
        this.photos = photos
      })
      .finally(() => (this.imgLoaded = true))
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
      this.$root.setAnimation(target.parentElement)
    },
    getRandomColor() {
      const random = () => Math.floor(Math.random() * 256)
      const r = random()
      const g = random()
      const b = random()
      return `rgba(${r}, ${g}, ${b}, 0.3)`
    },
  },
}
</script>

<style lang="scss" scoped>
.grid {
  display: grid;
  margin: 0 auto;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-auto-rows: minmax(200px, auto);
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
