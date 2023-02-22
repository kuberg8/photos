<template>
  <div class="grid">
    <VCard v-for="i in 18" :key="i" image="images/admin.jpg" title="Леша" link="detail" />
  </div>
</template>

<script>
import VCard from '~/components/VCard.vue'

export default {
  components: {
    VCard,
  },
}
</script>

<style lang="scss" scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); // 300 400 - min change column count
  grid-auto-rows: minmax(350px, auto);
  padding: 50px 7% 100px;
  column-gap: 15px;
  row-gap: 30px;
}
</style>
