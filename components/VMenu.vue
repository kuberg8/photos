<template>
  <aside>
    <h1 class="title">Наталья Епимахова <br />Фотограф</h1>

    <transition name="fade">
      <div v-if="folders.length" class="menu">
        <div class="item">
          <nuxt-link exact-active-class="active" to="/">Главная</nuxt-link>
        </div>

        <div v-show="folder.children.length" v-for="folder in folders" :key="folder.folderId">
          <VDropdown
            :title="folder.name"
            :links="folder.children"
            :id="folder.folderId"
          />
            <!-- v-if="folder.children.length" -->
          <!-- <nuxt-link v-else exact-active-class="active" :to="folder.folderPath">{{ folder.name }}</nuxt-link> -->
        </div>

        <div class="item">
          <nuxt-link exact-active-class="active" to="/price">Стоимость работы</nuxt-link>
        </div>
        <div class="item">
          <nuxt-link exact-active-class="active" to="/contacts">Контакты</nuxt-link>
        </div>
      </div>
    </transition>
  </aside>
</template>

<script>
import VDropdown from '~/components/VDropdown.vue'

export default {
  name: 'VMenu',
  components: {
    VDropdown,
  },
  props: {
    folders: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      dropdown: {
        count: 0,
        active: null,
      },
    }
  },
  provide() {
    return { dropdown: this.dropdown }
  },
}
</script>

<style lang="scss" scoped>
aside {
  background-color: #f5f5f5;
  padding: 50px;
  font-size: 10px;
  max-height: 100vh;
  position: sticky;
  top: 0;

  .menu {
    text-transform: uppercase;
    display: flex;
    flex-direction: column;
    row-gap: 29px;
  }

  .title {
    margin-bottom: 70px;
  }

  .item {
    width: auto;
  }

  @media screen and (max-width: 1280px) {
    display: none;
  }
}
</style>
