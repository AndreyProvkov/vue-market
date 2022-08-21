<template>
    <header class="header">
        <div class="wrapper">
            <div class="flex">
                <router-link to='/'>
                    <div class="logo">
                        <div class="logo__picture">
                            <img
                                class="logo__img"
                                src="@/assets/logo.svg"
                                alt="logo"
                            />
                        </div>
                        <p class="logo__text">
                            <span class="uppercase">ФЛАГ</span>&nbsp;Покупки
                        </p>
                    </div>
                </router-link>
                <a
                    class="btn"
                    @click="toggleModalWindow($event)"
                >
                    Регистрация
                </a>
            </div>
        </div> 
    </header>
</template>

<script>
export default {
    name: 'HeaderBar',
    methods: {
        toggleModalWindow (e) {
            this.$emit('toggleModalWindow', e)
        }
    }
}
</script>

<style scoped lang="scss">
%filter-drop-shadow {
    filter: drop-shadow(0 .4rem .2rem rgba(0, 0, 0, .25));
}
.flex {
    display: flex;
    justify-content: space-between;
    grid-column: 1 / 13;
}
a {
    text-decoration: none;
}
.header {
    background-color: #FFF;
    box-shadow: .2rem .4rem .8rem rgba(0, 0, 0, .1);
    padding: 1.7rem 0;
    margin-bottom: 2.4rem;
}
.logo {
    display: flex;
    align-items: center;
    grid-column: 1 / 4;
    position: relative;
    &::after {
            position: absolute;
            z-index: 1;
            width: 100%;
            height: 100%;
            content: '';
            top: 0;
            left: 0;
            background: url('@/assets/logo.svg') no-repeat;
        }
    &__picture {
        position: relative;
        margin-right: 1.9rem;
        width: 66px;
        height: 37px;
        @extend %filter-drop-shadow;
    }
    &__img {
        clip-path: polygon(0% 80%, 100% 80%, 100% 100%, 0% 100%);
    }
    &__text {
        color: #414141;
        font-weight: bold;
        margin: 0;
        @extend %filter-drop-shadow;
    }
}
</style>