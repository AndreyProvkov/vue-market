<template>
  <div
    :class="{item, 'item_wide': item.wide}"
    :key="item.id"
    v-for="item in catalogItems"
  >
    <span class="item__title">
      {{ item.title }}
    </span>
    <img
      class="item__img"
      :src="require(`@/assets/item_img/${item.img}`)"
    />
  </div>
</template>

<script>
export default {
  name: 'CatalogItem',
  props: {
    catalogItems: Array
  }
}
</script>

<style scoped lang="scss">
.item {
  grid-column: span 3;
  overflow: hidden;
  margin-bottom: 4rem;
  position: relative;
  cursor: pointer;
  background: #FFF;
  box-shadow: .1rem .2rem .4rem rgba(112, 192, 91, 0.2);
  border-radius: .4rem;
  &::after {
    position: absolute;
    content: '';
    background: linear-gradient(180deg, rgba(112, 192, 91, 0) 0%, #70C05B 82.81%);
    left: 0;
    right: 0;
    bottom: 0;
    height: 11.7rem;
  }
  &:hover {
    &::after {
      background: linear-gradient(180deg, rgba(255, 102, 51, 0) 0%, #FF6633 100%);
    }
  }
  &_wide {
    grid-column: span 6;
  }
  &__title {
    position: absolute;
    z-index: 1;
    left: 1rem;
    bottom: 1rem;
    right: 1rem;
    font-weight: 700;
    font-size: 1.8rem;
    color: #FFF;
  }
  &__img {
    object-fit: cover;
    width: 100%;
    height: 100%;
  }
}
</style>
