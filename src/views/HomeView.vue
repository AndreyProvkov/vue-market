<template>
    <h1>Главная</h1>
    <router-link to="/catalog">
        Каталог
    </router-link>
</template>

<script>
export default {
    name: 'HomeView'
}
</script>

<style scoped lang="scss">
h1 {
    grid-column: 1 / 13;
    margin: 0;
    margin-bottom: 2rem;
}
</style>