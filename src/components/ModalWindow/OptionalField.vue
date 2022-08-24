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
    </div>
</template>

<script>
export default {
    name: 'OptionalField'
}
</script>

<style scoped lang="scss">
.optional {
    display: grid;
    grid-template-columns: repeat(2, minmax(auto, 26rem));
    column-gap: 3.2rem;
    &__title {
        font-weight: 700;
        font-size: 1.8rem;
        grid-column: span 2;
        margin: 0;
        margin-bottom: 2.4rem;
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