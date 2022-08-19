<template>
  <HeaderBar />
  <div class='wrapper'>
    <BreadCrumb v-if="$route.name !== 'home'" />
    <router-view :catalogItems=catalogItems />
  </div>
</template>

<script>
import HeaderBar from '@/components/HeaderBar.vue'
import BreadCrumb from '@/components/BreadCrumb.vue';

export default {
  name: 'App',
  components: {
    HeaderBar,
    BreadCrumb,
  },
  data() {
    return {
      catalogItems: [
        {
          id: 1,
          title: 'Молоко, сыр, яйцо',
          wide: true,
          img: 'milk-eggs.jpg'
        },
        {
          id: 2,
          title: 'Хлеб',
          wide: false,
          img: 'bread.jpg'
        },
        {
          id: 3,
          title: 'Фрукты и овощи',
          wide: false,
          img: 'fruits-vegetables.jpg'
        },
        {
          id: 4,
          title: 'Бакалея',
          wide: false,
          img: 'grocery.jpg'
        },
        {
          id: 5,
          title: 'Здоровое питание',
          wide: false,
          img: 'healthy-eating.jpg'
        },
        {
          id: 6,
          title: 'Зоотовары',
          wide: true,
          img: 'pet-supplies.jpg'
        },
        {
          id: 7,
          title: 'Детское питание',
          wide: false,
          img: 'children-food.jpg'
        },
        {
          id: 8,
          title: 'Мясо, птица, колбаса',
          wide: true,
          img: 'meat.jpg'
        },
        {
          id: 9,
          title: 'Непродовольственные товары',
          wide: false,
          img: 'non-grocery-goods.jpg'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
@import url('@/assets/font/rubik/rubik.css');

html {
  font-size: 10px;
}

body {
  background: #F4F4F2;
  color: #414141;
  margin: 0;
  font-family: 'Rubik', Arial, Helvetica, sans-serif;
  font-size: 1.6rem;
  font-weight: 400;
  font-style: normal;
  line-height: 150%;
}

.wrapper {
  box-sizing: border-box;
  max-width: 128rem;
  margin: 0 auto;
  padding: 0 4rem;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-column-gap: 4rem;
}

.uppercase {
    text-transform: uppercase;
}

.btn {
  box-sizing: border-box;
  background: #70C05B;
  color: #FFFFFF;
  border-radius: .4rem;
  padding: .8rem 2rem;
  text-align: center;
  cursor: pointer;
  transition: .3s all;
  &:hover {
    background: #559245;
  }
}
</style>
