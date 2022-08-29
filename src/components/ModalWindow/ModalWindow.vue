<template>
    <div
        class="modal"
        data-modal="close"
        @click="toggleModalWindow($event)"
    >
        <div class="content">
            <button class="modal__close" data-modal="close">
                <svg class="modal__close-svg" width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M13.3536 0.646447C13.5488 0.841709 13.5488 1.15829 13.3536 1.35355L1.35355 13.3536C1.15829 13.5488 0.841709 13.5488 0.646447 13.3536C0.451184 13.1583 0.451184 12.8417 0.646447 12.6464L12.6464 0.646447C12.8417 0.451184 13.1583 0.451184 13.3536 0.646447Z"/>
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M0.646447 0.646447C0.841709 0.451184 1.15829 0.451184 1.35355 0.646447L13.3536 12.6464C13.5488 12.8417 13.5488 13.1583 13.3536 13.3536C13.1583 13.5488 12.8417 13.5488 12.6464 13.3536L0.646447 1.35355C0.451184 1.15829 0.451184 0.841709 0.646447 0.646447Z"/>
                </svg>
            </button>
            <RegistrationForm
                @submit="submit"
                @handlerInput="handlerInput"
                :errorsRegistryForm="errorsRegistryForm"
                v-if="!showSuccessRegistration"
            />
            <SuccessRegistration v-else />
        </div>
    </div>
</template>

<script>
import SuccessRegistration from './SuccessRegistration.vue'
import RegistrationForm from './RegistrationForm.vue'

export default {
    name: 'ModalWindow',
    components: {
    SuccessRegistration,
    RegistrationForm
    },
    props: {
        errorsRegistryForm: Object,
        showSuccessRegistration: Boolean
    },
    methods: {
        toggleModalWindow (e) {
            this.$emit('toggleModalWindow', e)
        },
        submit() {
            this.$emit('submit')
        },
        handlerInput (e) {
            this.$emit('handlerInput', e)
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
    &__close {
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
        &-svg {
            transition: .3s all;
            fill: #414141;
        }
        &:hover {
            background: #fdeeee;
        }
        &:hover .modal__close-svg {
            fill: red;
        }
    }
}
.content {
    background: #FFFFFF;
    margin: 0 3rem;
    box-shadow: .8rem 1.6rem 3.2rem rgba(255, 102, 51, 0.2);
    border-radius: .4rem;
    padding: 7.2rem 6.7rem 4rem;
    text-align: center;
    position: relative;
    overflow: hidden;
    max-height: 75vh;
    @media screen and (max-width: 550px) {
        padding: 5.2rem 1.7rem 3rem;
    }
}
</style>
