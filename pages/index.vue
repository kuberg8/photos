<template>
  <div class="index">
    <VIntro title="Natasha" :image="main" align-items="center" />

    <div class="container">
      <div class="block">
        <h1>С ЧЕГО НАЧАТЬ ЗНАКОМСТВО <br />С сайтом:</h1>
      </div>

      <hr class="block" />

      <!-- будет браться из приходящих папок первые 4 -->
      <div class="block">карточки</div>

      <hr class="block" />

      <div class="block form">
        <VCard :withGradient="false" image="example.jpeg" />

        <div class="info">
          <h1>КАК НАПИСАТЬ НАМ<br />ИЛИ ЗАДАТЬ ЛЮБОЙ ВОПРОС:</h1>

          <div>
            <b>TELEGRAM, WHAT'S APP И ЗВОНКИ</b>
            <div>
              8(999) 582 07 36 - Алексей Шульгин<br />@PAULINA.SHULGINA И @ALEXEY.SHULGIN - Соцсеть с доступом через VPN
            </div>
          </div>

          <div>
            <b>ДРУГИЕ СЕРВИСЫ</b>
            <div>boosty.to/shulginy - аккаунт BOOSTY</div>
          </div>

          <form @submit.prevent="() => {}" class="content">
            <div class="fields">
              <VInput v-model="name" name="name" placeholder="Ваше имя*" />
              <VInput v-model="phone" mask="+7 ### ### ##-##" name="phone" placeholder="Номер телефона*" />
              <VSelect v-model="askType" placeholder="Тип вопроса*" :options="asksOptions" />
              <VInput v-model="city" name="city" placeholder="Город*" />
              <VSelect v-model="workType" placeholder="Вид съемки*" :options="workOptions" />
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
          <a href="https://telegram.me/kuberg" target="_blank">@Kuberg</a>
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
      // будет браться из приходящих папок
      workOptions: ['Репортаж', 'Портретная', 'Парная', 'Свадебная'],
    }
  },
  mounted() {
    this.$root.setAnimation && this.$root.setAnimation()
  },
  computed: {
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

  .banner {
    margin-top: 100px;
    min-height: 423px;
    padding: 0 20%;

    .content {
      display: flex;
      flex-direction: column;
      row-gap: 20px;
    }
  }
}
</style>
