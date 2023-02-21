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
          <div class="text">{{ info.description }}</div>
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
          type: 'СТОИМОСТЬ РАБОТЫ',
          title: 'от 9 до 11 т.р./ час работы',
          description:
            'Стоимость работы зависит от продолжительности съемки, которая необходима для вашего формата торжества. Чаще всего это 4-5 часов для камерных, небольших свадеб (44-55 000 р.) , или 8-10 часов для объемных, продолжительных торжеств (88 - 110 000 р. соответственно).',
        },
        {
          type: 'МИНИМУМ И МАКСИМУМ ЧАСОВ РАБОТЫ',
          title: 'от 2-х часов работы и более',
          description:
            'Минимальное количество для заказа - от 2-х часов съемки в будние дни (с понедельника по четверг), от 7-ми часов и более в выходные дни и пятницы включительно. Максимальное количество часов ничем не ограничено.',
        },
        {
          type: 'КОЛИЧЕСТВО ФОТОГРАФИЙ',
          title: 'от 50 шт. за час работы',
          description:
            'Общее количество фотографий, которые вы получите в итоге, зависит от продолжительности и динамики съемки, но в среднем составляет около 50 шт. за один час. (следовательно, около 500 шт. за 10 часов съемки)',
        },
        {
          type: 'СРОКИ ГОТОВНОСТИ ФОТОГРАФИЙ',
          title: 'от 20 до 90 дней',
          description: 'В течение этого времени вы уже точно получите все фотографии. Раньше - возможно, позже - нет.',
        },
        {
          type: 'ДОПОЛНЕНИЯ И ПРИЯТНЫЕ БОНУСЫ',
          title: 'анонс и съёмка-знакомство',
          description:
            'Анонс в виде примерно 50 готовых фотографий со всего торжества вы получите в течение первых недель в любом случае, а при заказе более 9 часов нашей работы мы бесплатно проведём для вас съемку-знакомство ещё до свадебного торжества.',
        },
        {
          type: 'ГОРОДА, В КОТОРЫХ МЫ СНИМАЕМ',
          title: 'Южный Урал и вся Россия',
          description:
            'Чаще всего мы снимаем в Челябинске, и ближайших городах и площадках Урала, но при желании и доплате за транспортные расходы готовы приехать и прилететь в любую точку России.',
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
      font-size: 10px;
      letter-spacing: 2px;
    }
  }
}
</style>
