<template>
  <div>
    <VIntro :image="main" align-items="center" class="banner">
      <div class="content">
        <i>Чат в Telegram</i>
        <h1>
          <a href="https://telegram.me/kuberg" target="_blank">@Kuberg</a>
        </h1>
        <small> Подпишитесь, чтобы видеть обновления чаще, чем в других соцсетях </small>
      </div>
    </VIntro>

    <div class="grid block">
      <div class="item">
        <h2>Наши контакты</h2>

        <div>
          Вы можете связаться с нами любым удобным способом: в социальной сети, мессенджере или с помощью телефонного
          звонка. Почти все вопросы мы решаем равнозначно, но если вас интересует конкретная информация по занятости дат
          и бронированию - Алексей обладает большей компетенцией. И чаще проверяет сообщения.
        </div>

        <div>
          <b>ТЕЛЕФОН И МЕССЕНДЖЕРЫ</b>
          <div class="col">
            <small>+7 999 582 07 36 (Алексей)</small>
            <small>+7 999 584 37 28 (Полина)</small>
            <small>Telegram, What's App</small>
          </div>
        </div>

        <div>
          <b>СОЦИАЛЬНЫЕ СЕТИ И СТРАНИЦЫ:</b>
          <div class="col">
            <small>VK: @shulgina_wed (Полина)</small>
            <small>@shulgin_wed (Алексей)</small>
            <small>Канал Telegram: paulinashulgina</small>
          </div>
        </div>
      </div>

      <div class="item">
        <h2>Написать напрямую</h2>

        <form @submit.prevent="() => {}" class="form">
          <VInput v-model="name" name="name" placeholder="Ваше имя*" />
          <VTextarea v-model="message" name="message" placeholder="Вопрос или сообщение*" />
          <div>
            <button type="submit" :disabled="!name || !message">Отправить</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import VInput from '~/components/VInput.vue'
import VTextarea from '~/components/VTextarea.vue'

import main from '~/static/main.jpeg'

export default {
  components: {
    VInput,
    VTextarea,
  },
  mounted() {
    this.$root.setAnimation && this.$root.setAnimation()
  },
  data() {
    return {
      main,

      name: '',
      message: '',
    }
  },
}
</script>

<style lang="scss" scoped>
.banner {
  min-height: 423px;
  padding: 0 40%;

  .content {
    display: flex;
    flex-direction: column;
    row-gap: 20px;
    animation: translateY 1s;
  }
}

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
