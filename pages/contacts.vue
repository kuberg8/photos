<template>
  <div>
    <VIntro :image="main" align-items="center" class="banner">
      <div class="content">
        <i>Чат в Telegram</i>
        <h1>
          <a href="https://telegram.me/natata_lia" target="_blank">@natata_lia</a>
        </h1>
        <!-- <small> Подпишитесь, чтобы видеть обновления чаще, чем в других соцсетях </small> -->
      </div>
    </VIntro>

    <div class="grid block">
      <div class="item">
        <h2>Контакты</h2>

        <div>
          Вы можете связаться со мной любым удобным способом: в социальной сети, мессенджере или с помощью телефонного
          звонка. Почти все вопросы я решаю равнозначно.
        </div>

        <div>
          <b>ТЕЛЕФОН И МЕССЕНДЖЕРЫ</b>
          <div class="col">
            <small>+7 (952) 522 27-71 (Наталья)</small>
            <!-- <small>+7 999 584 37 28 (Полина)</small> -->
            <small>Telegram, What's App</small>
          </div>
        </div>

        <!-- <div>
          <b>СОЦИАЛЬНЫЕ СЕТИ И СТРАНИЦЫ:</b>
          <div class="col">
            <small>VK: @??</small>
          </div>
        </div> -->
      </div>

      <div class="item">
        <h2>Написать напрямую</h2>

        <form action="https://formspree.io/f/mgebazak" method="POST" class="form">
          <VInput v-model="name" name="name" placeholder="Ваше имя*" />
          <VInput v-model="phone" mask="+7 ### ### ##-##" name="phone" placeholder="Номер телефона*" />
          <VTextarea v-model="message" name="message" placeholder="Вопрос или сообщение*" />
          <div>
            <button type="submit" :disabled="!name || !message || !phone">Отправить</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import VInput from '~/components/VInput.vue'
import VTextarea from '~/components/VTextarea.vue'

import main from '~/static/main.jpg'

export default {
  components: {
    VInput,
    VTextarea,
  },
  mounted() {
    this.$root.setAnimation && this.$root.setAnimation()
  },
  head() {
    return {
      title: 'Контакты',
    }
  },
  data() {
    return {
      main,

      name: '',
      message: '',
      phone: ''
    }
  },
}
</script>

<style lang="scss" scoped>
.col {
  display: flex;
  flex-direction: column;
  row-gap: 10px;
  margin-top: 20px;
}

.form {
  display: flex;
  flex-direction: column;
  row-gap: 24px;
}

.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 64px;
  padding: 70px;

  .item {
    display: flex;
    flex-direction: column;
    row-gap: 48px;
  }
}
</style>
