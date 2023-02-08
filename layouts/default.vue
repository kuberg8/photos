<template>
  <main class="main">
    <VMenu />
    <Nuxt />
  </main>
</template>

<script>
import VMenu from '~/components/VMenu.vue'

export default {
  components: {
    VMenu,
  },
  mounted() {
    this.setAnimation()
    this.$root.setAnimation = this.setAnimation
  },
  methods: {
    setAnimation() {
      const blocks = document.querySelectorAll('.block')

      blocks.forEach((block) => {
        let exptl = this.$gsap.timeline({
          scrollTrigger: {
            trigger: block,
            start: 'top 95%',
            end: 'top 90%',
            scrub: 2,
            markers: false, // true for dev mode
          },
        })
        exptl.from(block, {
          y: 100,
          opacity: 0,
          stagger: 1,
          duration: 1,
        })
      })
    },
  },
}
</script>

<style lang="scss" scoped>
.main {
  display: grid;
  grid-template-columns: 300px auto;
  min-height: 100vh;
}
</style>
