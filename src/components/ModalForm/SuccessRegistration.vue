<template>
    <div class="success">
        <h2 class="success__title">
            Вы успешно зарегистрировались!
        </h2>
        <button
            type="button"
            class="btn-modal"
            data-modal="close"
            @click="toggleModalWindow($event)"
        >
            К покупкам
        </button>
    </div>
</template>

<script>
export default {
    name: 'SuccessRegistration',
    methods: {
        toggleModalWindow (e) {
            this.$emit('toggleModalWindow', e)
        }
    }
}
</script>

<style scoped lang="scss">
.success {
    min-width: 55.3rem;
    &__title {
        font-size: 2.4rem;
        color: #70C05B;
        max-width: 31.5rem;
        line-height: 150%;
        margin: 0 auto 4rem;
    }
}
</style>