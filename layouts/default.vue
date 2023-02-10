<template>
  <main class="main">
    <VMenu :folders="folders" />
    <Nuxt />
  </main>
</template>

<script>
import { mapMutations } from 'vuex'
import VMenu from '~/components/VMenu.vue'

export default {
  components: {
    VMenu,
  },
  mounted() {
    this.setAnimation()
    this.$root.setAnimation = this.setAnimation

    this.$axios.$get('/files?type=folder').then((data) => {
      this.folders = this.getFolderStructure(data)
      this.SET_SERVICES(this.folders)
    })
  },
  data() {
    return {
      folders: [],
    }
  },
  methods: {
    ...mapMutations(['SET_SERVICES']),
    setAnimation(el) {
      const blocks = el ? [el] : document.querySelectorAll('.block')

      blocks.forEach((block) => {
        let exptl = this.$gsap.timeline({
          scrollTrigger: {
            trigger: block,
            start: 'top 90%',
            end: 'top 95%',
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
    getFolderStructure(array = []) {
      return array
        .map((folder) => ({ ...folder, name: folder.name?.replaceAll('_', ' ') }))
        .reduce((tree, folder, i, mapedArray) => {
          folder.children = mapedArray.filter((childFolder) => {
            return childFolder.folderPath.includes(folder.folderPath) && folder.folderId !== childFolder.folderId
          })
          tree.push(folder)
          return tree
        }, [])
        .filter((folder) => !!folder.children.length || folder.folderPath.split('/').length < 3)
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
