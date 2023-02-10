<template>
  <div class="index">
    <VIntro title="indie - фотография" :image="main" align-items="center" />

    <div class="container">
      <div class="block">
        <h1>С ЧЕГО НАЧАТЬ ЗНАКОМСТВО <br />С сайтом:</h1>
      </div>

      <hr class="block" />

      <div class="block grid">
        <nuxt-link v-for="(item, i) in services" :key="i" :to="item.folderPath">{{ item.name }}</nuxt-link>
      </div>

      <hr class="block" />

      <div class="block form">
        <div>
          <VCard :withGradient="false" image="images/admin.jpg" style="max-height: 500px" />
        </div>

        <div class="info">
          <h1>КАК НАПИСАТЬ<br />ИЛИ ЗАДАТЬ ЛЮБОЙ ВОПРОС:</h1>

          <div>
            <b>TELEGRAM, WHAT'S APP И ЗВОНКИ</b>
            <div>+7 (952) 522 27-71 - Наталья Епимахова<br />@EPIMAHOVA_NATALIA - Соцсеть с доступом через VPN</div>
          </div>

          <div>
            <b>ДРУГИЕ СЕРВИСЫ</b>
            <div>boosty.to/shulginy - аккаунт BOOSTY ???</div>
          </div>

          <form action="https://formspree.io/f/mgebazak" class="content" method="POST">
            <div class="fields">
              <VInput v-model="name" name="name" placeholder="Ваше имя*" />
              <VInput v-model="phone" mask="+7 ### ### ##-##" name="phone" placeholder="Номер телефона*" />
              <VSelect v-model="askType" name="askType" placeholder="Тип вопроса*" :options="asksOptions" />
              <VInput v-model="city" name="city" placeholder="Город*" />
              <VSelect v-model="workType" name="workType" placeholder="Вид съемки*" :options="workOptions" />
            </div>

            <button type="submit" :disabled="!formValid"><i> Отправить </i></button>

            <small> *Отправляя форму, вы даёте согласие на обработку персональных данных. </small>
          </form>
        </div>
      </div>
    </div>

    <VIntro :image="main" align-items="center" class="banner">
      <div class="block content">
        <i>Чат в Telegram</i>
        <h1>
          <a href="https://telegram.me/natata_lia" target="_blank">@natata_lia</a>
        </h1>
        <small>
          Советуем подписаться: это остаётся самым стабильным способом первыми видеть обновления и следить за нашим
          творчеством. И его ещё никто не запретил!
        </small>
      </div>
    </VIntro>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import VIntro from '~/components/VIntro.vue'
import VInput from '~/components/VInput.vue'
import VSelect from '~/components/VSelect.vue'
import VCard from '~/components/VCard.vue'

import main from '~/static/main.jpeg'

export default {
  name: 'IndexPage',
  components: {
    VIntro,
    VInput,
    VCard,
    VSelect,
  },
  data() {
    return {
      main,

      name: '',
      phone: '',
      city: '',
      askType: '',
      workType: '',

      asksOptions: ['Занятость даты', 'Бронирование', 'Мне просто спросить', 'Другое'],
    }
  },
  mounted() {
    this.$root.setAnimation && this.$root.setAnimation()
  },
  head() {
    return {
      title: 'Главная',
    }
  },
  computed: {
    ...mapState(['services']),
    workOptions() {
      return this.services.map(({ name }) => name)
    },
    formValid() {
      return !!this.name && !!this.phone && !!this.city && !!this.askType && !!this.workType
    },
  },
}
</script>

<style lang="scss" scoped>
.index {
  text-align: center;
  padding-bottom: 100px;

  .container {
    padding: 50px 100px;
    display: flex;
    flex-direction: column;
    row-gap: 30px;
  }

  h1 {
    text-transform: uppercase;
    font-size: 25px;
  }

  .form {
    display: grid;
    grid-template-columns: 40% 50%;
    column-gap: 10%;
    text-align: left;

    .info {
      display: flex;
      flex-direction: column;
      row-gap: 48px;
      font-size: 11px;
      letter-spacing: 0.05em;
      line-height: 2;

      b {
        font-family: 'Arial';
      }
    }

    .fields {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 24px;
    }

    .content {
      display: flex;
      flex-direction: column;
      row-gap: 24px;
    }
  }

  .grid {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    column-gap: 50px;
  }
}
</style>
