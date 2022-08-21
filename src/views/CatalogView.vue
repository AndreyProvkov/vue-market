<template>
    <h1 class="title">Каталог</h1>
    <CatalogItem :catalogItems=catalogItems />
</template>

<script>
import CatalogItem from '@/components/CatalogItem.vue'

export default {
  name: 'CatalogView',
  components: {
    CatalogItem
  },
  props: {
    catalogItems: Array
  }
}
</script>

<style scoped lang="scss">
.title {
  margin: 0;
  font-size: 6.4rem;
  line-height: 150%;
  margin-bottom: 6rem;
}
</style>