<template>
    <div
        class="modal"
        data-modal="close"
        @click="toggleModalWindow($event)"
    >
        <div class="content">
            <SuccessRegistration />
            <button class="close" data-modal="close">
                <svg class="close__svg" width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M13.3536 0.646447C13.5488 0.841709 13.5488 1.15829 13.3536 1.35355L1.35355 13.3536C1.15829 13.5488 0.841709 13.5488 0.646447 13.3536C0.451184 13.1583 0.451184 12.8417 0.646447 12.6464L12.6464 0.646447C12.8417 0.451184 13.1583 0.451184 13.3536 0.646447Z"/>
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M0.646447 0.646447C0.841709 0.451184 1.15829 0.451184 1.35355 0.646447L13.3536 12.6464C13.5488 12.8417 13.5488 13.1583 13.3536 13.3536C13.1583 13.5488 12.8417 13.5488 12.6464 13.3536L0.646447 1.35355C0.451184 1.15829 0.451184 0.841709 0.646447 0.646447Z"/>
                </svg>
            </button>
            <h2 class="content__title">
                Регистрация
            </h2>
            <form class="form content__form">
                <p class="form__title">
                    Обязательные поля
                </p>
                <div class="left-side">
                    <label class="label">
                        Телефон
                        <input
                            class="input"
                            type="text"
                        />
                    </label>
                    <label class="label">
                        Фамилия
                        <input
                            class="input"
                            type="text"
                        />
                    </label>
                    <label class="label">
                        Имя
                        <input
                            class="input"
                            type="text"
                        />
                    </label>
                    <label class="label">
                        Пароль
                        <div class="label__password">
                            <input
                                class="input input__password"
                                type="text"
                            />
                            <button
                                class="btn-show-pass"
                                type="button"
                            ></button>
                        </div>
                    </label>
                    <label class="label">
                        Повторите пароль
                        <div class="label__password">
                            <input
                                class="input input__password"
                                type="text"
                            />
                            <button
                                class="btn-show-pass"
                                type="button"
                            ></button>
                        </div>
                    </label>
                </div>
                <div class="right-side">
                    <label class="label">
                        Дата рождения
                        <input
                            class="input"
                            type="text"
                        />
                    </label>
                    <label class="label">
                        Населенный пункт
                        <input
                            class="input"
                            type="text"
                        />
                    </label>
                    <div class="label">
                        <span class="label__text">
                            Пол
                        </span>
                        <div class="label__gender">
                            <input
                                checked
                                id="gender-man"
                                type="radio"
                                name="gender"
                                class="input__gender"
                            />
                            <label
                                class="label__radio-btn"
                                for="gender-man"
                            >
                                Мужской
                            </label>
                            <input
                                id="gender-woman"
                                type="radio"
                                name="gender"
                                class="input__gender"
                            />
                            <label
                                class="label__radio-btn"
                                for="gender-woman"
                            >
                                Женский
                            </label>
                        </div>
                    </div>
                </div>
                <p class="form__title">Необязательные поля</p>
                <div class="left-side">
                    <label class="label">
                        Номер карты
                        <input
                            class="input"
                            type="text"
                        />
                    </label>
                    <div class="label">
                        <input
                            id="no-card"
                            class="input__checkbox"
                            type="checkbox"
                        />
                        <label for="no-card" class="label__checkbox">
                            У меня нет карты лояльности
                        </label>
                    </div>
                </div>
                <div class="right-side">
                    <label class="label">
                        E-mail
                        <input
                            class="input"
                            type="text"
                        />
                    </label>
                </div>
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
    </div>
</template>

<script>
import SuccessRegistration from './SuccessRegistration.vue'

export default {
    name: 'ModalWindow',
    components: {
        SuccessRegistration
    },
    methods: {
        toggleModalWindow (e) {
            this.$emit('toggleModalWindow', e)
        }
    }
}
</script>

<style scoped lang="scss">
.modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    height: 100vh;
    width: 100vw;
    background-color: rgba(252, 213, 186, 0.8);
    z-index: 100;
    overflow: auto;
    display: flex;
    justify-content: center;
    align-items: center;
}
.content {
    background: #FFFFFF;
    box-shadow: .8rem 1.6rem 3.2rem rgba(255, 102, 51, 0.2);
    border-radius: .4rem;
    padding: 7.2rem 6.7rem 4rem;
    text-align: center;
    position: relative;
    overflow: hidden;
    max-height: 75vh;
    &__title {
        font-weight: 700;
        font-size: 2.4rem;
        margin: 0;
        margin-bottom: 4rem;
    }
}
.close {
    position: absolute;
    top: 0;
    right: 0;
    width: 4rem;
    height: 4rem;
    background: #F3F2F1;
    border-radius: .4rem;
    border: none;
    cursor: pointer;
    padding: 0;
    transition: .3s all;
    &__svg {
        transition: .3s all;
        fill: #414141;
    }
    &:hover {
        background: #fdeeee;
    }
    &:hover .close__svg {
        fill: red;
    }
}
.form {
    display: grid;
    grid-template-columns: repeat(2, minmax(auto, 26rem));
    column-gap: 3.2rem;
    overflow: auto;
    height: 90%;
    overscroll-behavior: contain;
    position: relative;
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
.left-side,
.right-side {
    margin-bottom: 4rem;
}
.label {
    display: block;
    text-align: left;
    color: #8F8F8F;
    margin-bottom: 1.6rem;
    &:last-child {
        margin: 0;
    }
    &__password {
        position: relative;
    }
    &__text {
        display: block;
    }
    &__gender {
        background: #F3F2F1;
        border-radius: 4px;
        padding: .4rem;
        display: flex;
    }
    &__radio-btn {
        font-weight: 400;
        font-size: 1.2rem;
        color: #414141;
        padding: .4rem .8rem;
        flex: 1 1 auto;
        align-items: center;
        text-align: center;
        cursor: pointer;
        border-radius: 4px;
        background: #F3F2F1;
        transition: .3s all;
    }
    &__checkbox {
        display: flex;
        align-items: center;
        cursor: pointer;
        &::before {
            content: '';
            display: inline-block;
            width: 2rem;
            height: 2rem;
            background: #FFFFFF;
            border: 1px solid #BFBFBF;
            border-radius: 4px;
            margin-right: .8rem;
        }
    }
}
.input {
    font-family: inherit;
    font-size: inherit;
    color: #414141;
    box-sizing: border-box;
    padding: .8rem 1.6rem;
    width: 100%;
    background: #FFFFFF;
    outline: none;
    border-radius: 4px;
    border: 1px solid #BFBFBF;
    transition: .3s all;
    &:focus {
        box-shadow: 4px 8px 16px rgba(112, 192, 91, 0.2);
        border: 1px solid #70C05B;
    }
    &__password {
        padding-right: 4rem;
    }
    &__gender {
        position: absolute;
        z-index: -1;
        opacity: 0;
        &:checked + .label__radio-btn {
            background: #70C05B;
            color: #fff;
        }
    }
    &__checkbox {
        position: absolute;
        z-index: -1;
        opacity: 0;
        &:checked + .label__checkbox::before {
            border-color: #0b76ef;
            background-color: #0b76ef;
            content: '✔';
            color: #fff;
            display: flex;
            align-items: center;
            justify-content: center;
        }
    }
}
.btn-show-pass {
    background: url("@/assets/icons/eye-off.svg") no-repeat center center;
    width: 2.4rem;
    height: 2.4rem;
    outline: none;
    border: none;
    cursor: pointer;
    background-color: transparent;
    position: absolute;
    top: 50%;
    right: .85rem;
    transform: translateY(-50%);
}
</style>
