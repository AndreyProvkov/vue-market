<template>
  <ModalWindow
    v-if="modalActive"
    @toggleModalWindow="toggleModalWindow($event)"
  />
  <HeaderBar @toggleModalWindow="toggleModalWindow($event)" />
  <div class='wrapper'>
    <BreadCrumb v-if="$route.name !== 'home'" />
    <router-view :catalogItems=catalogItems />
  </div>
</template>

<script>
import ModalWindow from '@/components/ModalWindow/ModalWindow.vue'
import HeaderBar from '@/components/HeaderBar.vue'
import BreadCrumb from '@/components/BreadCrumb.vue'

export default {
  name: 'App',
  components: {
    ModalWindow,
    HeaderBar,
    BreadCrumb
  },
  data() {
    return {
      modalActive: false,
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
  },
  methods: {
    toggleModalWindow (e) {
      const el = e.target
      if (el.dataset.modal === 'open') {
        this.modalActive = true
      }
      if (el.dataset.modal === 'close') {
        this.modalActive = false
      }
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
  max-width: 120rem;
  margin: 0 auto;
  padding: 0 4rem;
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

.btn-modal {
  font-family: inherit;
  cursor: pointer;
  position: relative;
  z-index: 1;
  background: #FCD5BA;
  border-radius: 4px;
  padding: 1.6rem;
  width: 100%;
  max-width: 26rem;
  font-size: 2.4rem;
  color: #FF6633;
  border: none;
  transition: .3s all;
  &:hover {
    background: #ffe5d2;
  }
}
</style>
