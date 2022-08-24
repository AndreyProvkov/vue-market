<template>
    <div class="registration">
        <h2 class="registration__title">
            Регистрация
        </h2>
        <form
            class="form"
            @submit.prevent="submit"
        >
            <RequiredField />
            <OptionalField />
            <div class="form__btn">
                <button
                    class="btn-modal"
                    type="submit"
                >
                    Продолжить
                </button>
            </div>
        </form>
    </div>
</template>

<script>
import RequiredField from './RequiredField.vue'
import OptionalField from './OptionalField.vue'

export default {
    name: "RegistrationForm",
    components: { 
        RequiredField,
        OptionalField
    },
    methods: {
        submit () {
            this.$emit('submit', true)
        }
    }
}
</script>

<style scoped lang="scss">
.registration {
    &__title {
        font-weight: 700;
        font-size: 2.4rem;
        margin: 0;
        margin-bottom: 4rem;
    }
}
.form {
    overflow: auto;
    overscroll-behavior: contain;
    height: 67.5vh;
    &__title {
        font-weight: 700;
        font-size: 1.8rem;
        grid-column: span 2;
        margin: 0;
        margin-bottom: 2.4rem;
    }
    &__btn {
        width: 100%;
        grid-column: span 2;
        position: sticky;
        bottom: 0;
        &::after {
            position: absolute;
            content: "";
            background: linear-gradient(180deg, rgba(255, 255, 255, 0) 0%, #ffffff 50%);
            left: 0;
            right: 0;
            bottom: 0;
            height: 6rem;
        }
    }
}
</style>