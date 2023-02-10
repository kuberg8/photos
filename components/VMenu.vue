<template>
  <aside>
    <h1 class="title">Наташин сайт ^__^</h1>

    <transition name="fade">
      <div v-if="folders.length" class="menu">
        <div class="item">
          <router-link exact-active-class="active" to="/">Главная</router-link>
        </div>

        <div v-for="folder in folders" :key="folder.folderId">
          <VDropdown
            v-if="folder.children.length"
            :title="folder.name"
            :links="folder.children"
            :id="folder.folderId"
          />
          <router-link v-else exact-active-class="active" :to="folder.folderPath">{{ folder.name }}</router-link>
        </div>

        <div class="item">
          <router-link exact-active-class="active" to="/price">Стоимость работы</router-link>
        </div>
        <div class="item">
          <router-link exact-active-class="active" to="/contacts">Контакты</router-link>
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
  text-transform: uppercase;
  max-height: 100vh;
  position: sticky;
  top: 0;

  .menu {
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
