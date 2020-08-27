<template>
<div class="container">
  <div class="leftPanel"><menubar /></div>
  
  <div class="container-login"> 
    <form class="newClient" @submit.prevent="submitHandler">
      <div class="newCardClient">
        <h1 class="card-title">Создание нового клиента</h1>
      
        <div class="input-field">          
          <input id="nameLast" type="text" v-model.trim="nameLast" @blur="$v.nameLast.$touch()" :class="{invalid: $v.nameLast.$dirty && !$v.nameLast.required}">    
          <span class="bar"></span> 
          <label for="nameLast">Фамилия: </label>  
          <small class="helper-text invalid" v-if="!$v.nameLast.required">
            Введите фамилию
          </small>
        </div>

        <div class="input-field">          
          <input id="nameFirst" type="text" v-model.trim="nameFirst" @blur="$v.nameFirst.$touch()" :class="{invalid: $v.nameFirst.$dirty && !$v.nameFirst.required}"> 
          <span class="bar"></span>
          <label for="nameFirst">Имя: </label>       
          <small class="helper-text invalid" v-if="!$v.nameFirst.required">
            Введите имя
          </small>
        </div>

        <div class="input-field">          
          <input id="name" type="text" v-model.trim="nameFath">
          <span class="bar"></span>
          <label for="name">Отчество: </label>
        </div>

        <div class="input-field">          
          <input id="birthDay" type="date" v-model.trim="birthDay" @blur="$v.birthDay.$touch()" :class="{invalid: ($v.birthDay.$dirty && !$v.birthDay.required )}">
          <span class="bar"></span>        
          <label for="name">Дата рождения: </label>
          <small class="helper-text invalid" v-if="!$v.birthDay.required">
            Введите дату
          </small>
        </div>
        <div class="messageSending">
        <div class="input-field">          
          <input id="phoneNumber" v-model.trim="phoneNumber" @blur="$v.phoneNumber.$touch()" :class="{invalid: ($v.phoneNumber.$dirty && !$v.phoneNumber.required) || ($v.phoneNumber.$dirty && $v.phoneNumber.$invalid)}">  
          <span class="bar"></span>
          <label for="name">Номер телефона: </label>      
          <small class="helper-text invalid" v-if="!$v.phoneNumber.required">
            Введите номер телефона 
          </small>
          <small class="helper-text invalid" v-if="$v.phoneNumber.$dirty && $v.phoneNumber.$invalid">
            Номер телефона должен состоять из 11 символов, начиная с 7
          </small>
        </div>
        <div class="input-field">  
          <input type="checkbox" class="checkbox" v-model="sendMessage" />
              <label for="checkbox">Не отправлять смс</label>
        </div>

        </div>

        <div class="input-field">          
           <div class="input-sex">
             <span>Пол: </span>
             <input type="radio" id="male" value="Мужчина" v-model="sex">
              <p for="male">Мужина </p>
            <input type="radio" id="female" value="Жещина" v-model="sex">
              <p for="female">Женщина </p>
             </div>
        </div> 

       <div class="input-field">
         <label for="clientGroup">Группа клиентов: </label>
         <span class="bar"></span>
         <select v-model="clientGroup" @blur="$v.clientGroup.$touch()" :class="{invalid: !$v.clientGroup.required}" multiple>
           <option>VIP</option>
           <option>Проблемные</option>
           <option>ОМС</option>
         </select>
         <span>Выбрано: {{ clientGroup }}</span>
         <br>
         <small class="helper-text" v-if="!$v.clientGroup.required">
            Поле обязательно для заполнения
          </small>
       </div>

        <div class="input-field">
          <label for="doctor">Лечащий врач: </label>
          <span class="bar"></span>
          <select v-model="doctor">
            <option disabled value="">Выберите один из вариантов</option>
            <option>Иванов</option>
            <option>Захаров</option>
            <option>Чернышева</option>
          </select>
        </div>   

          

        <div class="input-field">          
          <input id="post" v-model.trim="post">  
          <span class="bar"></span>      
          <label for="post">Индекс: </label>
        </div>

        <div class="input-field">          
          <input id="country" v-model.trim="country">   
          <span class="bar"></span>      
          <label for="country">Страна: </label>
        </div>

        <div class="input-field">          
          <input id="region" v-model.trim="region"> 
          <span class="bar"></span>  
          <label for="region">Область: </label>       
        </div>

        <div class="input-field">          
          <input id="city" v-model.trim="city" @blur="$v.city.$touch()" :class="{invalid: ($v.city.$dirty && !$v.city.required )}">   
          <span class="bar"></span>  
          <label for="city">Город: </label>     
          <small class="helper-text invalid" v-if="!$v.city.required">
            Введите город
          </small>
        </div>

        <div class="input-field">         
          <input id="street" v-model.trim="street"> 
          <span class="bar"></span>
          <label for="street">Улица: </label>         
        </div>

        <div class="input-field">          
          <input id="house" v-model.trim="house">  
          <span class="bar"></span>
          <label for="house">Дом: </label>        
        </div>

        <div class="input-field">
          <label for="documentType">Тип документа: </label>
          <select v-model="documentType" @blur="$v.documentType.$touch()" :class="{invalid: (!$v.documentType.required)}">
            <option disabled value="">Выберите один из вариантов</option>
            <option>Паспорт</option>
            <option>Свидетельство о рождении</option>
            <option>Водительское удостоверение</option>
          </select>
          <small class="helper-text invalid" v-if="!$v.documentType.$required">
              Выберите документ
            </small>
        </div>

        <div class="input-field">          
          <input id="passportData" type="text" v-model="passportData" @blur="$v.passportData.$touch()" :class="{invalid: (!$v.passportData.required && $v.passportData.$invalid)}">
          <span class="bar"></span>
          <label for="passportData">Введите серию и номер паспорта: </label>  
          <small class="helper-text invalid" v-if="!$v.passportData.$required">
              Введите данные
            </small>
            <small class="helper-text invalid" v-if="$v.passportData.$dirty && $v.passportData.$invalid">
              Серия и номер паспорта должны быть в формате 1234 567890
            </small>
        </div>

        <div class="input-field">          
          <input id="documentRelease" v-model.trim="documentRelease">
          <span class="bar"></span>
          <label for="documentRelease">Кем выдан: </label>   
        </div>

        <div class="input-field">          
          <input type="date" id="passportDate" v-model="passportDate" @blur="$v.passportDate.$touch()" :class="{invalid: (!$v.passportDate.required)}">
          <span class="bar"></span> 
          <label for="passportDate">Дата выдачи: </label> 
          <small class="helper-text invalid" v-if="!$v.passportDate.$required">
              Введите дату
            </small>
        </div>

        <div class="card-action">
          <div>
            
            <button class="btn" type="submit" :disabled="$v.$invalid">
              Зарегистрировать
            </button>
          </div>
        </div>
      </div>
    </form>
  </div>
</div>
</template>

<script>
import {email, required, minLength} from 'vuelidate/lib/validators'
import menubar from '@/components/menubar'



export default {
  name: 'register',
  data: () => ({
    nameFirst: '',
    nameLast: '',
    nameFath:'',
    birthDay: null,
    phoneNumber: null,
    sex: null,    
    clientGroup: [],
    doctor: '',
    sendMessage: true,
    post: '',
    country: '',
    region: '',
    city: '',
    street: '',
    house: '',
    documentType: '',
    passportData: null,
    documentRelease: '',
    passportDate: null
  }),
  validations: {
    nameFirst: {required},
    nameLast: {required},    
    birthDay: {required},
    phoneNumber: {required, validFormat: val => /^[7][0-9]{10}$/.test(val)},
    clientGroup: {required},
    sendMessage: {checked: v => v},
    city: {required},
    documentType: {required},
    passportData: {
      required,
      validFormat: val => /^\d{4} \d{6}$/.test(val),
    },
    passportDate:{required}
  },
  methods: {
    submitHandler() {      
      const formData = {
        nameLast: this.nameLast,
        nameFirst: this.nameFirst,
        nameFath: this.nameFath,
        birthDay: this.birthDay,
        phoneNumber: this.phoneNumber,
        sex: this.sex,
        clientGroup: this.clientGroup,
        doctor: this.doctor,        
        sendMessage: this.sendMessage,
        post: this.post,
        country: this.country,
        region: this.region,
        city: this.city,
        street: this.street,
        house: this.house,
        documentType: this.documentType,
        passportData: this.passportData,
        documentRelease: this.documentRelease,
        passportDate: this.passportDate
      }

       if (this.$v.$invalid) {
        this.$v.$touch()
        alert('Исправьте ошибки')
       } else {
      console.log(formData);
      alert('Работа выполнена');
       }
      
      

    },
  },
    components: {
      menubar
  }
}
</script>

<style lang="scss">
*{
	margin: 0;
	padding: 0;
}

body {
	font-size: 16px;
}
.container {
 display: grid;
 grid-template-columns: 300px 1fr;
}

@media (max-width: 900px) {
  .container{
    display: flex;
  }
  .container-login{
  position: absolute;
  }

  .input-sex{
    display: flex;
  }

}


.container-login {
  width: 95%;  
  min-height: 100vh;
  display: -webkit-box;
  display: -webkit-flex;
  display: -moz-box;
  display: -ms-flexbox;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background: #fff;  
}

.newClient {
  width: 100%;
  display: block;
  color: #333333;
  .helper-text{
    color:red;
  }
}

.card-title {
  font-size: 24px;
  color: rgba(0, 0, 0, 0.849);
  text-align: center;
  margin: 30px;
}

.input-field {
  position: relative;
  margin-bottom: 30px;
}

.input-sex{
  display: inline-flex;
  text-align: center;
  
  p{
    color: #999;
    font-size: 18px;
    margin: 0 15px;
  }
}

span{
  color: #999;
  font-size: 18px;
  margin: 0 10px;

 }
.checkbox {
	z-index: auto;
	opacity: 0;
	margin: 10px 0 0 20px;
}
.checkbox + label {
	position: relative;
	padding: 0 0 0 60px;
	cursor: pointer;
}
.checkbox + label:before {
	content: '';
	position: absolute;
	top: -4px;
	left: 0;
	width: 50px;
	height: 92%;
	border-radius: 13px;
	background: #CDD1DA;
	box-shadow: inset 0 2px 3px rgba(0,0,0,.2);
	transition: .2s;
}
.checkbox + label:after {
	content: '';
	position: absolute;
	top: -2px;
	left: 2px;
	width: 22px;
	height: 75%;
	border-radius: 10px;
	background: #FFF;
	box-shadow: 0 2px 5px rgba(0,0,0,.3);
	transition: .2s;
}
.checkbox:checked + label:before {
	background: #9FD468;
}
.checkbox:checked + label:after {
	left: 26px;
}
.checkbox:focus + label:before {
	box-shadow: inset 0 2px 3px rgba(0,0,0,.2), 0 0 0 3px rgba(255,255,0,.7);
}


input {
  font-size: 16px;
  padding: 10px;
  display: block;
  width: 100%;
  border: none;
  border-bottom: 1px solid #ccc;
}
input:focus {
  outline: none;
}

label {
  color: #999;
  font-size: 18px;
  position: absolute;
  pointer-events: none;
  left: 10px;
  top: -15px;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}

input:focus ~ label {
  top: -15px;
  font-size: 14px;
  color: #5264AE;
}

 select {
    font-size: 16px;
    padding: 10px;
    display: block;
    width: 100%;
    border: none;
    border-bottom: 1px solid #ccc;
    text-align: center;
   }

.bar {
  position: relative;
  display: block;
  width: 100%;
}
.bar:before, .bar:after {
  content: "";
  height: 2px;
  width: 0;
  bottom: 0;
  position: absolute;
  background: #5264AE;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}
.bar:before {
  left: 50%;
}
.bar:after {
  right: 50%;
}

input:focus ~ .bar:before,
input:focus ~ .bar:after {
  width: 50%;
}

.messageSending {
  display: inline-flex;
  width: 100%;
  .input-field{
    width: 50%;
  }
}


button {
  display: block;
  cursor: pointer;
  outline: none;  
  background-color: #018b5d;
  color: #ccc;
  border-radius: 30px;
  font-size: 20px;
  font-weight: 600;
  padding: 10px;
  background-size: 100% 100%;
  text-align: center;
  margin: auto;
  position: relative;
}

  :disabled{
    background-color: #8b010cd5;
  }


</style>