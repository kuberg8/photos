<template>
  <aside>
    <h1 class="title">Наташин сайт ^__^</h1>
    <div class="item">
      <router-link exact-active-class="active" to="/">Главная</router-link>
    </div>

    <VDropDown
      title="Портфолио"
      :links="[
        { url: '/couples', text: 'Пары' },
        { url: '/portraits', text: 'Индивидуальные съемки' },
        { url: '/couples3', text: 'Пары' },
      ]"
    />

    <div class="item">
      <router-link exact-active-class="active" to="/price">Стоимость работы</router-link>
    </div>
    <div class="item">
      <router-link exact-active-class="active" to="/contacts">Контакты</router-link>
    </div>
  </aside>
</template>

<script>
import VDropDown from '~/components/VDropDown.vue'

export default {
  name: 'VMenu',
  components: {
    VDropDown,
  },
}
</script>

<style lang="scss" scoped>
aside {
  display: flex;
  flex-direction: column;
  row-gap: 29px;
  background-color: #f5f5f5;
  padding: 50px;
  font-size: 10px;
  text-transform: uppercase;
  max-height: 100vh;
  position: sticky;
  top: 0;

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
