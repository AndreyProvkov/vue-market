<template>
    <div class="required">
        <p class="required__title">
            Обязательные поля
        </p>
        <div class="left-side">
            <label class="label">
                Телефон
                <input
                    class="input"
                    :class="{'input_error': !!errorsRegistryForm.phone}"
                    type="text"
                    name="phone"
                    v-model="phoneNumber"
                    @input="handlerInput"
                />
                <span class="label__error">
                    {{errorsRegistryForm.phone}}
                </span>
            </label>
            <label class="label">
                Фамилия
                <input
                    class="input"
                    :class="{'input_error': !!errorsRegistryForm.surname}"
                    type="text"
                    name="surname"
                    v-model="surname"
                    @input="handlerInput"
                />
                <span class="label__error">
                    {{errorsRegistryForm.surname}}
                </span>
            </label>
            <label class="label">
                Имя
                <input
                    class="input"
                    :class="{'input_error': !!errorsRegistryForm.firstName}"
                    type="text"
                    name="firstName"
                    v-model="firstName"
                    @input="handlerInput"
                />
                <span class="label__error">
                    {{errorsRegistryForm.firstName}}
                </span>
            </label>
            <label class="label">
                Пароль
                <div class="label__password">
                    <input
                        class="input input__password"
                        :class="{'input_error': !!errorsRegistryForm.password}"
                        type="password"
                        name="password"
                        v-model="password"
                        @input="handlerInput"
                    />
                    <button
                        class="btn-show-pass"
                        type="button"
                        @mouseup="hidePass($event)"
                        @mousedown="showPass($event)"
                    ></button>
                    <span class="label__error">
                        {{errorsRegistryForm.password}}
                    </span>
                </div>
            </label>
            <label class="label">
                Повторите пароль
                <div class="label__password">
                    <input
                        class="input input__password"
                        :class="{'input_error': !!errorsRegistryForm.passwordRepeat}"
                        type="password"
                        name="passwordRepeat"
                        v-model="passwordRepeat"
                        @input="handlerInput"
                    />
                    <button
                        class="btn-show-pass"
                        type="button"
                        @mouseup="hidePass($event)"
                        @mousedown="showPass($event)"
                    ></button>
                    <span class="label__error">
                        {{errorsRegistryForm.passwordRepeat}}
                    </span>
                </div>
            </label>
        </div>
        <div class="right-side">
            <label class="label">
                Дата рождения
                <input
                    class="input"
                    :class="{'input_error': !!errorsRegistryForm.birthday}"
                    type="date"
                    name="birthday"
                    v-model="birthday"
                    @input="handlerInput"
                    @blur="handlerInput"
                />
                <span class="label__error">
                    {{errorsRegistryForm.birthday}}
                </span>
            </label>
            <label class="label">
                Населенный пункт
                <vue-dadata
                    v-model="city"
                    :token="token"
                    :locationOptions="constraints"
                    fromBound="city"
                    toBound="city"
                    :autocomplete="true"
                    inputName="city"
                    :class="{'vue-dadata_error': !!errorsRegistryForm.city}"
                />
                <span class="label__error">
                    {{errorsRegistryForm.city}}
                </span>
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
                        v-model="gender"
                        value="male"
                        @change="handlerInput"
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
                        v-model="gender"
                        value="female"
                        @change="handlerInput"
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
    </div>
</template>

<script>
import { ref } from 'vue';
import { VueDadata } from 'vue-dadata';

export default {
    name: 'RequiredField',
    components: {
        VueDadata
    },
    props: {
        errorsRegistryForm: Object
    },
    data () {
        return {
            phone: '',
            birthday: '',
            firstName: '',
            surname: '',
            gender: 'male',
            password: '',
            passwordRepeat: ''
        }
    },
    setup() {
        const city = ref('');

        return {
            token: '70984f274702eaf96bba357b60b21b82897d39ec',
            city,
            constraints: {
                locations: { 
                    region_fias_id: "92b30014-4d52-4e2e-892d-928142b924bf" 
                },
            },
        }
    },
    methods: {
        handlerInput(e) {
            const el = e.target
            const value = el.value
           
            if (el.name === 'phone') {
                this.inputNumber()
            }

            if (el.name === 'surname' || el.name === 'firstName') {
                this.inputName(el, value)
            }

            if (el.name === 'password') {
                this.inputPass()
            }

            if (el.name === 'passwordRepeat') {
                this.inputPass()
            }

            if (el.name === 'birthday') {
                this.inputBirthday(e)
            }

            this.$emit('handlerInput', {name: el.name, str: this[el.name]})
        },
        inputNumber() {
            this.phone = this.phone.replace(/\D/g, '')

            if (this.phone.length > 11) {
                this.phone = this.phone.slice(0, 11)
            }
        },
        inputName(el, value) {
            value = value.replace(/[^а-яёА-ЯЁ]/g,"")

            if (value) {
                value = value[0].toUpperCase() + value.slice(1)
            }

            this[el.name] = value
        },
        inputPass() {
            this.password = this.password.replace(/[а-яёА-ЯЁ]|\s+/gi, '')
        },
        inputBirthday(e) {
            const date = new Date()
            const currentYear = date.getFullYear()

            const birthdayArr = this.birthday.split('-')

            if (birthdayArr[0].length >= 4) {
                if (birthdayArr[0] > currentYear) {
                    birthdayArr[0] = currentYear
                }
            }

            if (e.type === 'blur') {
                if (birthdayArr[0] && birthdayArr[0] < 1920) {
                    birthdayArr[0] = 1920
                }
            }

            this.birthday = birthdayArr.join('-')
        },
        hidePass(e) {
            e.target.previousElementSibling.type = 'password'
        },
        showPass(e) {
            e.target.previousElementSibling.type = 'text'
        }
    },
    watch: {
        city (val) {
            this.$emit('handlerInput', {name: 'city', str: val})
        }
    },
    computed: { 
        phoneNumber: {
            get () {
                const x = this.phone.match(/(\d{0,1})(\d{0,3})(\d{0,3})(\d{0,2})(\d{0,2})/)
                x[1] = '+7'
                return !x[3] ? x[1] + ' ' + x[2] : x[1] + ' ' + x[2] + ' ' + x[3] + (x[4] ? '-' + x[4] : '') + (x[5] ? '-' + x[5] : '')
            },
            set (val) {
                this.phone = val
            }
        }
    }
}
</script>

<style scoped lang="scss">
.required {
    display: grid;
    grid-template-columns: repeat(2, minmax(10rem, 26rem));
    column-gap: 3.2rem;
    &__title {
        font-weight: 700;
        font-size: 1.8rem;
        grid-column: span 2;
        margin: 0;
        margin-bottom: 2.4rem;
        @media screen and (max-width: 550px) {
            grid-column: span 1;
        }
    }
    @media screen and (max-width: 550px) {
        grid-template-columns: 1fr
    }
}
.left-side,
.right-side {
    margin-bottom: 4rem;
    @media screen and (max-width: 550px) {
        margin: 0;
    }
}
.right-side {
    @media screen and (max-width: 550px) {
        margin-bottom: 3rem;
    }
}
.label {
    display: block;
    text-align: left;
    color: #8F8F8F;
    margin-bottom: 1.6rem;
    position: relative;
    @media screen and (max-width: 550px) {
        width: 85%;
        margin: 0 auto 1.6rem;
    }
    &:last-child {
        margin: 0;
        @media screen and (max-width: 550px) {
            margin: 0 auto;
        }
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
    &__error {
        position: absolute;
        left: 0;
        bottom: -2rem;
        font-size: 1rem;
        color: red;
    }
}
.vue-dadata__input {
    font-family: inherit;
    font-size: inherit;
    color: #414141 !important;
    box-sizing: border-box;
    padding: .8rem 1.6rem !important;
    width: 100%;
    background: #FFFFFF !important;
    outline: none;
    border-radius: 4px !important;
    border: 1px solid #BFBFBF !important;
    transition: .3s all;
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
    &_error {
        &:focus {
            box-shadow: 4px 8px 16px rgba(192, 91, 91, 0.2);
            border: 1px solid red;
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