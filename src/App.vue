<template>
  <ModalWindow
    v-if="modalActive"
    @toggleModalWindow="toggleModalWindow($event)"
    @handlerInput="handlerInput"
    @submit="submit"
    :errorsRegistryForm="errorsRegistryForm"
    :showSuccessRegistration="showSuccessRegistration"
  />
  <HeaderBar @toggleModalWindow="toggleModalWindow($event)" />
  <div class='wrapper'>
    <BreadCrumb v-if="$route.name !== 'home'" />
    <router-view :catalogItems=catalogItems />
  </div>
</template>

<script>
import ModalWindow from '@/components/ModalWindow/ModalWindow.vue'
import HeaderBar from '@/components/HeaderBar.vue'
import BreadCrumb from '@/components/BreadCrumb.vue'

export default {
  name: 'App',
  components: {
    ModalWindow,
    HeaderBar,
    BreadCrumb
  },
  data() {
    return {
      showSuccessRegistration: false,
      modalActive: false,
      registryForm: {
        phone: '',
        birthday: '',
        firstName: '',
        surname: '',
        gender: 'male',
        city: '',
        password: '',
        passwordRepeat: '',
        card: '',
        email: '',
        isNoCard: false
      },
      errorsRegistryForm: {
        phone: '',
        birthday: '',
        firstName: '',
        surname: '',
        city: '',
        password: '',
        passwordRepeat: '',
        card: '',
        email: ''
      },
      errors: {
        phone: {
          length: 'Неверная длина номера'
        },
        name: {
          length: 'Минимальная длина слова 3 буквы'
        },
        password: {
          length: 'Минимальная длина пароля 5 символов',
          capitalLetter: 'Пароль должен содержать заглавную букву',
          lowercaseLetter: 'Пароль должен содержать строчную букву',
          number: 'Пароль должен содержать цифру'
        },
        repeatPassword: {
          similar: 'Пароли не совпадают'
        },
        birthday: {
          date: 'Дата должна быть в формате dd.mm.yyyy',
          maxYear: `Указанный год не может быть больше ${new Date().getFullYear()}`,
          minYear: 'Указанный год не может быть меньше 1920'
        },
        city: {
          input: 'Поле не заполнено'
        },
        card: {
          length: 'Номер карты должен состоять из 8-ми цифр'
        },
        email: {
          format: 'Email должен быть в формате *@*.*'
        }
      },
      catalogItems: [
        {
          id: 1,
          title: 'Молоко, сыр, яйцо',
          wide: true,
          img: 'milk-eggs.jpg'
        },
        {
          id: 2,
          title: 'Хлеб',
          wide: false,
          img: 'bread.jpg'
        },
        {
          id: 3,
          title: 'Фрукты и овощи',
          wide: false,
          img: 'fruits-vegetables.jpg'
        },
        {
          id: 4,
          title: 'Бакалея',
          wide: false,
          img: 'grocery.jpg'
        },
        {
          id: 5,
          title: 'Здоровое питание',
          wide: false,
          img: 'healthy-eating.jpg'
        },
        {
          id: 6,
          title: 'Зоотовары',
          wide: true,
          img: 'pet-supplies.jpg'
        },
        {
          id: 7,
          title: 'Детское питание',
          wide: false,
          img: 'children-food.jpg'
        },
        {
          id: 8,
          title: 'Мясо, птица, колбаса',
          wide: true,
          img: 'meat.jpg'
        },
        {
          id: 9,
          title: 'Непродовольственные товары',
          wide: false,
          img: 'non-grocery-goods.jpg'
        }
      ]
    }
  },
  methods: {
    toggleModalWindow (e) {
      const el = e.target
      if (el.dataset.modal === 'open') {
        this.modalActive = true
      }
      if (el.dataset.modal === 'close' || el.closest('.modal__close')) {
        this.modalActive = false
        this.showSuccessRegistration = false
      }
    },
    handlerInput ({name, str}) {
      this.registryForm[name] = str

      if (name === 'phone') {
        this.checkNumber()
      }

      if (name === 'firstName' || name === 'surname') {
        this.checkName(name)
      }

      if (name === 'password') {
        this.checkPass()
        this.checkPasswordRepeat()
      }

      if (name === 'passwordRepeat') {
        this.checkPasswordRepeat()
      }

      if (name === 'birthday') {
        this.checkBirthday()
      }

      if (name === 'city') {
        this.checkCity()
      }

      if (name === 'card') {
        this.checkCard()
      }

      if (name === 'email') {
        this.checkEmail()
      }
    },
    checkNumber() {
      if (this.registryForm.phone.length < 11) {
        this.errorsRegistryForm.phone = this.errors.phone.length
      } else {
        this.errorsRegistryForm.phone = ''
      }
    },
    checkName(name) {
      if (this.registryForm[name].length < 3) {
        this.errorsRegistryForm[name] = this.errors.name.length
      } else {
        this.errorsRegistryForm[name] = ''
      }
    },
    checkPass() {
      if (this.registryForm.password.length < 5) {
        this.errorsRegistryForm.password = this.errors.password.length
      } else if (!/(?=.*[a-z])/.test(this.registryForm.password)) {
        this.errorsRegistryForm.password = this.errors.password.lowercaseLetter
      } else if (!/(?=.*[A-Z])/.test(this.registryForm.password)) {
        this.errorsRegistryForm.password = this.errors.password.capitalLetter
      } else if (!/(?=.*[0-9])/.test(this.registryForm.password)) {
        this.errorsRegistryForm.password = this.errors.password.number
      } else {
        this.errorsRegistryForm.password = ''
      }
    },
    checkPasswordRepeat() {
      if (this.registryForm.passwordRepeat !== this.registryForm.password) {
        this.errorsRegistryForm.passwordRepeat = this.errors.repeatPassword.similar
      } else {
        this.errorsRegistryForm.passwordRepeat = ''
      }
    },
    checkBirthday() {
      const date = new Date()
      const currentYear = date.getFullYear()
      const birthdayArr = this.registryForm.birthday.split('-')

      if (this.registryForm.birthday === '') {
        this.errorsRegistryForm.birthday = this.errors.birthday.date
      } else if (birthdayArr[0] > currentYear) {
        this.errorsRegistryForm.birthday = this.errors.birthday.maxYear
      } else if (birthdayArr[0] < 1920) {
        this.errorsRegistryForm.birthday = this.errors.birthday.minYear
      } else {
        this.errorsRegistryForm.birthday = ''
      }
    },
    checkCity() {
      if (this.registryForm.city === '') {
        this.errorsRegistryForm.city = this.errors.city.input
      } else {
        this.errorsRegistryForm.city = ''
      }
    },
    checkCard() {
      if (this.registryForm.card.length > 0 && this.registryForm.card.length < 9) {
        this.errorsRegistryForm.card = this.errors.card.length
      } else {
        this.errorsRegistryForm.card = ''
      }
    },
    checkEmail () {
      if (!/.+@.+\..+/i.test(this.registryForm.email) && this.registryForm.email.length > 0) {
        this.errorsRegistryForm.email = this.errors.email.format
      } else {
        this.errorsRegistryForm.email = ''
      }
    }
  }
}
</script>

<style lang="scss">
@import url('@/assets/font/rubik/rubik.css');

html {
  font-size: 10px;
}

body {
  background: #F4F4F2;
  color: #414141;
  margin: 0;
  font-family: 'Rubik', Arial, Helvetica, sans-serif;
  font-size: 1.6rem;
  font-weight: 400;
  font-style: normal;
  line-height: 150%;
}

.wrapper {
  max-width: 120rem;
  margin: 0 auto;
  padding: 0 4rem;
}

.uppercase {
  text-transform: uppercase;
}

.btn {
  box-sizing: border-box;
  background: #70C05B;
  color: #FFFFFF;
  border-radius: .4rem;
  padding: .8rem 2rem;
  text-align: center;
  cursor: pointer;
  transition: .3s all;
  &:hover {
    background: #559245;
  }
}

.btn-modal {
  font-family: inherit;
  cursor: pointer;
  position: relative;
  z-index: 1;
  background: #FCD5BA;
  border-radius: 4px;
  padding: 1.6rem;
  width: 100%;
  max-width: 26rem;
  font-size: 2.4rem;
  color: #FF6633;
  border: none;
  transition: .3s all;
  &:hover {
    background: #ffe5d2;
  }
}

.vue-dadata {
  position: relative;
  &__input {
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
  }
  &__suggestions {
    position:absolute;
    z-index:1;
    width:100%;
    display:flex;
    flex-direction:column;
    background-color:#fff;
    &-item {
      padding:10px;
      cursor:pointer;
      transition:.3s;
      &:hover {
        background-color:#ffdfbd;
      }
      &_current {
        background-color:#fff5e7;
      }
    }
  }
}
</style>
