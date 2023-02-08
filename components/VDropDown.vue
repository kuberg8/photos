<template>
  <div>
    <div class="a" :class="{ active: isOpen }" @click="isOpen = !isOpen">{{ title }}</div>

    <transition name="fade">
      <div v-if="isOpen" class="wrapper">
        <div class="dropdown">
          <router-link v-for="(link, i) in links" :key="i" active-class="active" :to="link.url">
            {{ link.text }}
          </router-link>
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
  },
  data() {
    return {
      isOpen: false,
    }
  },
  watch: {
    '$route.path': {
      handler(path) {
        if (this.links.some(({ url }) => path.includes(url))) this.isOpen = true
        else this.isOpen = false
      },
      immediate: true,
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
}
</style>

<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s;
  max-height: 230px;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
  max-height: 0px;
}
</style>
