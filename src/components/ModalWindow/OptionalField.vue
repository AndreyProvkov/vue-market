<template>
    <div class="optional">
        <p class="optional__title">
            Необязательные поля
        </p>
        <div class="left-side">
            <label class="label">
                Номер карты
                <input
                    class="input"
                    type="text"
                    name="card"
                    v-model="card"
                    @input="handlerInput"
                />
            </label>
            <div class="label">
                <input
                    id="no-card"
                    class="input__checkbox"
                    type="checkbox"
                    v-model="isNoCard"
                    @change="handlerInput"
                />
                <label
                    for="no-card"
                    class="label__checkbox"
                >
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
                    name="email"
                    v-model="email"
                    @input="handlerInput"
                />
            </label>
        </div>
    </div>
</template>

<script>
export default {
    name: 'OptionalField',
    data () {
        return {
            card: '',
            email: '',
            isNoCard: false
        }
    },
    methods: {
        handlerInput(e) {
            const el = e.target

            if (el.name === 'card') {
                this.inputCard()
            }

            this.$emit('handlerInput', {name: el.name, str: this[el.name]})
        },
        inputCard () {
            this.card = this.card.replace(/\D/g, '')
            if (this.card.length > 2) {
                this.card = this.card.slice(0, 2) + '-' + this.card.slice(2)
            }
            if (this.card.length > 9) {
                this.card = this.card.slice(0, 9)
            }
        },
        checkEmail () {
            let validEmail = /.+@.+\..+/i.test(this.email)
            console.log(validEmail)
        }
    }
}
</script>

<style scoped lang="scss">
.optional {
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
.left-side {
    @media screen and (max-width: 550px) {
        margin-bottom: 1.6rem;
    }
}
.label {
    display: block;
    text-align: left;
    color: #8F8F8F;
    margin-bottom: 1.6rem;
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
    &__checkbox {
        display: flex;
        align-items: center;
        cursor: pointer;
        &::before {
            content: '';
            flex: 0 0 auto;
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
</style>