<template>
  <div>
    <VIntro :image="price" align-items="center" class="banner">
      <div class="content">
        <h1>Условия и стоимость съемки</h1>
      </div>
    </VIntro>

    <div class="price">
      <div class="grid">
        <div v-for="(info, i) in priceInfo" :key="i" class="card">
          <small>{{ info.type }}</small>
          <h1>{{ info.title }}</h1>
          <hr />
          <div class="text" v-html="info.description" />
        </div>
      </div>

      <div class="block">
        <nuxt-link class="link" to="/contacts">ЗАКАЗАТЬ СЪЕМКУ ИЛИ ЗАДАТЬ ВОПРОС</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import price from '~/static/images/price.jpg'
import VIntro from '~/components/VIntro.vue'

export default {
  components: {
    VIntro,
  },
  mounted() {
    this.$root.setAnimation && this.$root.setAnimation()
  },
  head() {
    return {
      title: 'Стоимость работ',
    }
  },
  data() {
    return {
      price,

      priceInfo: [
        {
          type: 'Индивидуальная съёмка',
          title: '3000 ₽',
          description: `Может проводиться на открытом воздухе или в любой закрытой локации. Подготовка к съемке включает в себя составление концепции, подбор одежды, выбор локации. 
            <ul>
            <li>От 30 до 40 кадров в полной обработке</li>
            <li>Полная готовность до 10 дней</li>
            <li>Получение ссылки на скачивание в электронном формате.</li>
            </ul>
            <br>
            Дополнительно может потребоваться оплата аренды локации и/или услуг визажиста.`,
        },
        {
          type: 'Съёмка для пары/семейная съёмка',
          title: '3000 ₽',
          description: `Может проводиться на открытом воздухе или в любой закрытой локации.
Подготовка к съемке включает в себя составление концепции, подбор одежды, выбор локации.
<ul>
<li>От 40 до 60 кадров в полной обработке</li>
<li>Полная готовность до 14 дней</li>
<li>Получение ссылки на скачивание в электронном формате.</li>
</ul>`,
        },
        {
          type: 'Свадебная съёмка',
          title: '3000 ₽/час',
          description: `Все условия обговариваются индивидуально, для получения точной информации можно связаться со мной любым удобным способом`,
        },
      ],
    }
  },
}
</script>

<style lang="scss" scoped>
.price {
  display: flex;
  flex-direction: column;
  row-gap: 70px;
  align-items: center;
  padding: 70px 70px 150px;

  .grid {
    display: grid;
    margin: 0 auto;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    column-gap: 50px;
    row-gap: 80px;
  }

  .card {
    display: flex;
    flex-direction: column;
    row-gap: 10px;
    font-weight: 400;
    animation: translateY 1s;

    .text {
      word-spacing: 10px;
      line-height: 25px;
    }

    small {
      text-transform: uppercase;
      font-size: 10px;
      letter-spacing: 2px;
    }
  }
}
</style>
