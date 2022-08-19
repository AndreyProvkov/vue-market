<template>
  <HeaderBar />
  <div class='wrapper'>
    <BreadCrumb />
    <router-view/>
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
}

.wrapper {
  max-width: 120.8rem;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-column-gap: 4rem;
}

.uppercase {
    text-transform: uppercase;
}
</style>
