<template>
  <div>
    <div class="a" :class="{ active: visible }" @click="open">{{ title }}</div>

    <transition name="fade">
      <div v-if="visible" class="wrapper">
        <div class="dropdown">
          <nuxt-link v-for="link in links" :key="link.folderId" active-class="active" :to="link.folderPath">
            {{ link.name }}
          </nuxt-link>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: '',
    },
    links: {
      type: Array,
      default: () => [],
    },
    id: {
      type: String,
      default: null,
      require: true,
    },
  },
  created() {
    this.index = this.dropdown.count++
  },
  mounted() {
    if (this.isSamePath()) {
      this.dropdown.active = this.index
    }
  },
  inject: ['dropdown'],
  computed: {
    visible() {
      return this.index === this.dropdown.active
    },
  },
  methods: {
    open() {
      if (this.visible) {
        this.dropdown.active = null
      } else {
        this.dropdown.active = this.index
      }
    },
    isSamePath() {
      return this.links.some(({ folderPath }) => {
        return decodeURIComponent(this.$route.path) === folderPath
      })
    },
  },
  watch: {
    '$route.path'() {
      if (this.isSamePath()) {
        this.dropdown.active = this.index
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.dropdown {
  display: flex;
  flex-direction: column;
  row-gap: 17.5px;
  padding-top: 25px;

  a {
    text-transform: none;
  }
}

.wrapper {
  overflow: hidden;
  will-change: max-height;
}
</style>

<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s;
  max-height: 150px;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
  max-height: 0px;
}
</style>
