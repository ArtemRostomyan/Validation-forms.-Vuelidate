<template>
  <div id="app">
    <form action="">
      <transition name="bounce">
        <div 
          v-show="screen === 1"
          class="reg-box">
          <label class="reg-box__text" for="name">Имя</label>
          <input
              @blur="$v.name.$touch()"
              v-model.trim="$v.name.$model" 
              class="reg-box__input" 
              :class="{'reg-box__input--error': $v.name.$error}"
              id="name"  
              type="text"
              autocomplete="off">
            
            <p
              v-if="!$v.name.required"
              class="error-text">{{requiredText}}</p>
            <p
              v-if="!$v.name.alpha"
              class="error-text">{{alphaText}}</p>
            <label class="reg-box__text" for="surname">Фамилия</label>
            <input 
                @blur="$v.surname.$touch()"
                v-model="$v.surname.$model"
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.surname.$error}"
                id="surname"  
                type="text"
                autocomplete="off">
            <p
              v-if="!$v.surname.required"
              class="error-text">{{requiredText}}</p>
            <p
              v-if="!$v.surname.alpha"
              class="error-text">{{alphaText}}</p>
            <label class="reg-box__text" for="birth">Дата рождения</label>
            <input
                @blur="$v.birth.$touch()"
                v-model="$v.birth.$model" 
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.birth.$error}"
                id="birth" 
                type="date"
                min="1865-01-01"
                autocomplete="off">
              <p
                  v-if="!$v.birth.required"
                  class="error-text">{{requiredText}}</p>
          <button 
                @click="nextScreen"
                :class="{'disabledBtn' : disabledBtn1}"
                :disabled="disabledBtn1"
                type="button" 
                class="btn">{{nextWord}}</button>
        </div>
      </transition>
      <!-- screen2 -->
      <transition name="bounce">
        <div 
            v-show="screen === 2"
            class="reg-box">
            <label class="reg-box__text" for="login">Логин</label>
            <input 
                @blur="$v.login.$touch()"
                v-model="$v.login.$model" 
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.login.$error}"
                id="login"  
                type="text"
                autocomplete="off">
            <p
              v-if="!$v.login.required"
              class="error-text">{{requiredText}}</p>
            <p
                v-if="!$v.login.minLength"
                class="error-text">{{minLengthText}} 5 символов</p>
            <p
                v-if="!$v.login.alphaNum"
                class="error-text">Только буквы цифры и тире</p>
            
            <label class="reg-box__text " for="password">Пароль</label>
            <input 
                @blur="$v.password.$touch()"
                v-model="$v.password.$model" 
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.password.$error}" 
                id="password"  
                type="password"
                autocomplete="off">
              <p
                v-if="!$v.password.required"
                class="error-text">{{requiredText}}</p>
              <p
                v-if="!$v.password.minLength"
                class="error-text">{{minLengthText}} 6 символов</p>
            <label class="reg-box__text" for="passwordToo">Повторите пароль</label>
            <input 
                @blur="$v.passwordToo.$touch()"
                v-model="$v.passwordToo.$model" 
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.passwordToo.$error}"  
                id="passwordToo" 
                type="password"
                >
            <p
                v-if="!$v.passwordToo.required"
                class="error-text">{{requiredText}}</p>
            <p
                v-if="!$v.passwordToo.sameAs"
                class="error-text">{{sameAsText}}</p>
            <div class="button-box">
              <button 
                @click="backScreen"
                type="button" 
                class="btn">{{backWord}}</button>
              <button 
                @click="nextScreen"
                :class="{'disabledBtn' : disabledBtn2}"
                :disabled="disabledBtn2"
                type="button" 
                class="btn">{{nextWord}}</button>
            </div>
        </div>
      </transition>
      <!-- screen3 -->
      <transition name="bounce">
        <div 
            v-show="screen === 3"
            class="reg-box">
            <label class="reg-box__text" for="country">Страна</label>
            <input 
                @blur="$v.country.$touch()"
                v-model="$v.country.$model" 
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.country.$error}" 
                id="country"  
                type="text"
                autocomplete="off">
            <p
              v-if="!$v.country.alpha"
              class="error-text">{{alphaText}}</p>
            <label class="reg-box__text " for="city">Город</label>
            <input 
                @blur="$v.city.$touch()"
                v-model="$v.city.$model" 
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.city.$error}" 
                id="city"  
                type="text"
                autocomplete="off">
            <p
              v-if="!$v.city.alpha"
              class="error-text">{{alphaText}}</p>
            <label class="reg-box__text" for="controlWord">Контрольное слово</label><span class="reg-box__subtext">(Запомните для получения доступа к аккаунту)</span>
            <input 
                @blur="$v.controlWord.$touch()"
                v-model="$v.controlWord.$model" 
                class="reg-box__input" 
                :class="{'reg-box__input--error': $v.controlWord.$error}" 
                id="controlWord" 
                type="text"
                autocomplete="off"
                >
            <p
              v-if="!$v.controlWord.required"
              class="error-text">{{requiredText}}</p>
            <p
              v-if="!$v.controlWord.alpha"
              class="error-text">{{alphaText}}</p>
            <p
                v-if="!$v.controlWord.minLength"
                class="error-text">{{minLengthText}} 3 символа</p>
            <div class="button-box">
              <button 
                @click="backScreen"
                type="button" 
                class="btn">{{backWord}}</button>
              <button 
                  :class="{'disabledBtn' : disabledBtn3}"
                  :disabled="disabledBtn3"
                  @click="registration"
                  type="button" 
                  class="btn">{{registrationWord}}</button>
            </div>
        </div>
      </transition>
    </form>
  </div>
</template>

<script>
import { required, minLength, sameAs, helpers } from 'vuelidate/lib/validators'
const alpha = helpers.regex('alpha', /^[a-zA-Zа-яёА-ЯЁ]*$/)
const alphaNum = helpers.regex('alphaNum', /^[a-zA-Zа-яёА-ЯЁ0-9_-]*$/)

export default {
  name: 'app',
  data () {
    return {
      screen: 1,
      backWord: 'Назад',
      nextWord: 'Далее',
      registrationWord: 'Зарегестрироваться',
      requiredText: 'Заполните поле',
      alphaText: 'В поле не должно содержаться цифр и других символов',
      sameAsText: 'Пароли не совпадают',
      minLengthText: 'Поле должно содержать минимум ',
      name: '',
      surname: '',
      birth: '',
      login: '',
      password: '',
      passwordToo: '',
      country: '',
      city: '',
      controlWord: ''
    }
  },
  methods: {
    nextScreen(){
        if(this.screen < 3){
        this.screen++
        }

      
      
    },
    backScreen(){
      if(this.screen > 1){
        this.screen--
      }
      
    },
    registration(){
      if(this.screen === 3){
        alert('Регистрация прошла успешно')
      }
      
    },
    
    
  },
  computed: {
    disabledBtn1(){
      return  this.$v.name.$invalid ||
              this.$v.surname.$invalid ||
              this.$v.birth.$invalid 
    },
    disabledBtn2(){
      return  this.$v.login.$invalid ||
              this.$v.password.$invalid ||
              this.$v.passwordToo.$invalid 
    },
    disabledBtn3(){
      return  this.$v.name.$invalid ||
              this.$v.surname.$invalid ||
              this.$v.birth.$invalid ||
              this.$v.login.$invalid ||
              this.$v.password.$invalid ||
              this.$v.passwordToo.$invalid ||
              this.$v.country.$invalid ||
              this.$v.city.$invalid ||
              this.$v.controlWord.$invalid 
    },
  },
  validations: {
    name: {
      required,
      alpha
    },
    surname: {
      required,
      alpha
    },
    birth: {
      required
    },
    login: {
      alphaNum,
      required,
      minLength: minLength(5)
    },
    password: {
      required,
      minLength: minLength(6)
    },
    passwordToo: {
      required,
      sameAs: sameAs('password')
    },
    country: {
      alpha
    },
    city: {
      alpha
    },
    controlWord: {
      required,
      alpha,
      minLength: minLength(3)
    }
  }
}
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  outline: none;
}
html{
  width: 100%;
  height: 100%;
}
body{
  font-family: Arial, Helvetica, sans-serif;
  width: 100%;
  height: 100%;
  background-color: rgb(253, 253, 253);
  display: flex;
  justify-content: center;
  align-items: center;
}
button{
  &:disabled{
    color: #000;
  }
}
.button-box{
  width: 100%;
  display: flex;
  flex-direction: column;
}
.btn{
  background-color: #fff;
  min-width: 40%;
  padding: 10px 10px;
  height: 50px;
  border-radius: 10px;
  margin: 5px auto;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 25px;
  border: 2px solid #000;
  cursor: pointer;
  transition: 0.4s;
  &:hover,
    :focus{
    background-color: #000;
    color: #fff;
  }
  &:active{
    opacity: 0.7;
  }
}
.disabledBtn{
  cursor: default;
   &:hover,
    :focus{
      background-color: #fff;
      color: #000;
  }
  &:active{
    opacity: 1;
  }
}
.error-text{
  margin: 0 0 5px 5px;
  color: red;
}
.reg-box{
  background-color: rgb(255, 233, 37);
  display: flex;
  flex-direction: column;
  width: 450px;
  min-height: 350px;
  border-radius: 15px;
  padding: 10px;
  &__input{
    padding-left: 5px;
    color: #000;
    font-size: 18px;
    font-weight: 500;
    width: 100%;
    height: 45px;
    border-radius: 7px;
    background-color: rgb(245, 245, 245);
    border: 3px solid rgb(245, 245, 245);
    transition: 0.2s;
    margin: 10px 0;
    &:first-child{
      margin-top: 25px;
    }
    &:focus{
      background-color: #fff;
      border: 3px solid rgb(0, 0, 0);
    }
    &--error{
      border: 3px solid red;
      &:focus{
        border: 3px solid red;
      }
    }
  }
  &__text{
    margin-left: 5px;
    font-weight: 500;
    color: rgb(59, 58, 58);
    font-size: 18px;
    font-family: Arial, Helvetica, sans-serif;
    cursor: pointer;
    &:first-child{
      margin-top: 4px;
    }
  }
  &__subtext{
    margin-left: 5px;
    font-weight: 300;
    font-size: 15px;
    color: rgb(73, 72, 72);
  }
  
}
@media(max-width: 480px){
  body{
    background-color: #ffcaca;
  }
  .reg-box{
    justify-content: center;
    background-color: #ffe925;
    display: flex;
    flex-direction: column;
    width: 282px;
    min-height: 447px;
    border-radius: 15px;
    padding: 10px;
  }
  .btn{
    min-width: 54%;
  }
}
@media(max-height: 480px){
  body{
    background-color: #ffcaca;
  }
  .reg-box{
    justify-content: center;
    background-color: #ffe925;
    display: flex;
    flex-direction: column;
    width: 515px;
    min-height: 400px;
    border-radius: 15px;
    padding: 10px;
  }
  .button-box{
    display: flex;
    justify-content: space-between;
    flex-direction: row;
  }
  .btn{
    
  }
}
.bounce-enter-active {
  animation: bounce-in .5s ;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}
</style>
