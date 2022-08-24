<template>
    <ul class="breadcrumb">
        <li class="breadcrumb__item">Главная</li>
        <li class="breadcrumb__item">Каталог</li>
    </ul>
</template>

<script>
export default {
    name: 'BreadCrumb'
}
</script>

<style scoped lang="scss">
.breadcrumb {
    list-style: none;
    color: #414141;
    font-size: 1.2rem;
    margin: 0;
    margin-bottom: 2.4rem;
    padding: 0;
    &__item {
        display: inline-block;
        &:not(:last-child) {
            position: relative;
            margin-right: 4.8rem;
            &::after {
                content: '';
                position: absolute;
                right: -2.4rem;
                top: 50%;
                width: .8rem;
                height: .8rem;
                transform: translateY(-50%) rotate(45deg);
                border: .1rem solid #414141;
                border-left: none;
                border-bottom: none;
            }
        }
        &:last-child {
            color: #8F8F8F;
        }
    }
}
</style>