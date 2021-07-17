<template>
  <div class="create-client">
    <h1 class="create-client__header">Создать клиента</h1>

    <form @submit.prevent="submit">
      <section class="basic">
        <div class="input">
          <p class="input__text">Фамилия <span>*</span></p>
          <input
            class="input__input"
            type="text"
            v-model.trim="surname"
            :class="{ invalid: $v.surname.$dirty && !$v.surname.required }"
          />
          <span class="error" v-if="$v.surname.$dirty && !$v.surname.required"
            >Необходимо ввести фамилию</span
          >
        </div>

        <div class="input">
          <p class="input__text">Имя <span>*</span></p>
          <input
            class="input__input"
            type="text"
            v-model.trim="name"
            :class="{ invalid: $v.name.$dirty && !$v.name.required }"
          />
          <span class="error" v-if="$v.name.$dirty && !$v.name.required"
            >Необходимо ввести имя</span
          >
        </div>
        <div class="input">
          <p class="input__text">Отчество</p>
          <input class="input__input" type="text" />
        </div>
        <div class="input">
          <p class="input__text">Дата рождения <span>*</span></p>
          <input
            class="input__input"
            type="date"
            v-model.trim="birthday"
            :class="{ invalid: $v.birthday.$dirty && !$v.birthday.required }"
          />
          <span class="error" v-if="$v.birthday.$dirty && !$v.birthday.required"
            >Необходимо ввести дату рождения</span
          >
        </div>
        <div class="input">
          <p class="input__text">Номер телефона <span>*</span></p>
          <input
            class="input__input"
            type="tel"
            v-model.trim="tel"
            :class="{
              invalid:
                ($v.tel.$dirty && !$v.tel.required) ||
                !$v.tel.maxLength ||
                !$v.tel.minLength,
            }"
          />
          <span class="error" v-if="$v.tel.$dirty && !$v.tel.required"
            >Необходимо ввести номер телефона</span
          >
          <span
            class="error"
            v-else-if="
              ($v.tel.$dirty && !$v.tel.maxLength) || !$v.tel.minLength
            "
            >Номер должен содержать 11 цифр</span
          >
          <span class="error" v-else-if="$v.tel.$dirty && !$v.tel.telFormat"
            >Номер должен начинаться с 7</span
          >
        </div>

        <!-- <Input
          type="tel"
          maxlength="11"
          pattern="^\+?[78][-\(]?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$"
          text="Номер телефона"
          required
        /> -->
        <div class="input">
          <p class="input__text">Пол</p>
          <div class="input__input-area">
            <label
              >Мужской
              <input class="input__radio" type="radio" name="sex" value="man" />
            </label>
            <label
              >Женский
              <input
                class="input__radio"
                type="radio"
                name="sex"
                value="woman"
              />
            </label>
          </div>
        </div>
        <div class="input">
          <p class="input__text">Группа клиентов <span>*</span></p>
          <select
            class="input__select"
            multiple
            size="1"
            name="group"
            v-model.trim="group"
            :class="{
              invalid: $v.group.$dirty && !$v.group.required,
            }"
          >
            <option value="vip">VIP</option>
            <option value="trouble">Проблемные</option>
            <option value="insurance">ОМС</option>
          </select>
          <span class="error" v-if="$v.group.$dirty && !$v.group.required"
            >Необходимо выбрать группу клиента</span
          >
        </div>
        <div class="input">
          <p class="input__text">Лечащий врач</p>
          <select class="input__input" surname="physician">
            <option value="Ivanov">Иванов</option>
            <option value="Zaharov">Захаров</option>
            <option value="Chernysheva">Чернышева</option>
          </select>
        </div>
        <div class="input">
          <label class="input__text"
            >Не отправлять СМС <input type="checkbox" surname="sms" />
          </label>
        </div>
      </section>
      <h2 class="create-client__subheader">Адрес</h2>
      <section class="address">
        <Input type="number" text="Индекс" />
        <Input type="text" text="Страна" />
        <Input type="text" text="Область" />
        <div class="input">
          <p class="input__text">Город <span>*</span></p>
          <input
            class="input__input"
            type="text"
            v-model.trim="city"
            :class="{ invalid: $v.city.$dirty && !$v.city.required }"
          />
          <span class="error" v-if="$v.city.$dirty && !$v.city.required"
            >Необходимо ввести город</span
          >
        </div>
        <Input type="text" text="Улица" />
        <Input type="number" text="Дом" />
      </section>
      <h2 class="create-client__subheader">Паспорт</h2>
      <section class="document">
        <div class="input">
          <p class="input__text">Тип документа <span>*</span></p>
          <select
            class="input__input"
            surname="document-type"
            v-model.trim="document"
            :class="{
              invalid: $v.document.$dirty && !$v.document.required,
            }"
          >
            <option value="passport">Паспорт</option>
            <option value="birth-certificate">Свидетельство о рождении</option>
            <option value="driver-license">Вод. удостоверение</option>
          </select>
          <span class="error" v-if="$v.document.$dirty && !$v.document.required"
            >Необходимо выбрать тип документа</span
          >
        </div>
        <Input type="number" text="Серия" />
        <Input type="number" text="Номер" />
        <Input type="text" text="Кем выдан" />
        <div class="input">
          <p class="input__text">Дата выдачи <span>*</span></p>
          <input
            class="input__input"
            type="date"
            v-model.trim="issueDate"
            :class="{ invalid: $v.issueDate.$dirty && !$v.issueDate.required }"
          />
          <span
            class="error"
            v-if="$v.issueDate.$dirty && !$v.issueDate.required"
            >Необходимо ввести дату рождения</span
          >
        </div>
      </section>
      <div class="submit-wrapper">
        <button
          class="submit"
          type="submit"
          :disabled="submitStatus === 'PENDING'"
        >
          Создать
        </button>
        <p class="modal ok" v-if="submitStatus === 'OK'">Клиент создан!</p>
        <p class="modal err" v-if="submitStatus === 'ERROR'">
          Форма заполнена неверно!
        </p>
        <!-- <p class="modal" v-if="submitStatus === 'PENDING'">Ожидание...</p> -->
      </div>
    </form>
  </div>
</template>
<script>
import Input from "@/components/Input.vue";
import { validationMixin } from "vuelidate";
import { required, maxLength, minLength } from "vuelidate/lib/validators";
const telFormat = (value) => value[0] == 7;
export default {
  mixins: [validationMixin],

  name: "App",
  components: {
    Input,
  },
  validations: {
    surname: { required },
    name: { required },
    birthday: { required },
    tel: {
      required,
      maxLength: maxLength(11),
      minLength: minLength(11),
      telFormat,
    },
    group: {
      required,
    },
    city: { required },
    document: { required },
    issueDate: { required },
  },
  data: () => ({
    surname: "",
    name: "",
    birthday: "",
    tel: "",
    group: "",
    city: "",
    document: "",
    issueDate: "",
  }),

  methods: {
    submit() {
      console.log("submit!");
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        // this.submitStatus = "PENDING";
        // setTimeout(() => {
        this.submitStatus = "OK";
        // }, 500);
      }
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@400;700&display=swap");
* {
  font-family: "Rubik", sans-serif;
  font-size: 16px;
  color: #646d8f;
}
.create-client {
  max-width: 1200px;
  margin: 0 auto;
  background: #eef0f8;
  border-radius: 15px;
  position: relative;

  &__header {
    text-align: center;
    font-size: 40px;
    font-weight: 400;
  }

  &__subheader {
    text-align: center;
    font-size: 25px;
    font-weight: 400;
    margin: 2%;
  }
}
.input__select {
  border-radius: 5px;
  box-shadow: 0px 0px 2px 1px #646d8f;
  outline: none;
  border: none;
  width: 300px;
}
.input__input-area {
  width: 300px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.address,
.basic,
.document {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.submit-wrapper {
  display: flex;
  justify-content: center;
}
.submit {
  width: 200px;
  background: linear-gradient(135deg, #7ceaae 30%, #52c898 100%);
  border-radius: 15px;
  outline: none;
  border: none;
  padding: 2%;
  margin: 2%;
  font-size: 20px;
  color: #eef0f8;
  cursor: pointer;
}
.submit:hover {
  box-shadow: 0px 0px 2px 1px #52c898;
}
.modal {
  position: absolute;
  top: 35%;
  right: 35%;
  width: 300px;
  background: #eef0f8;
  border-radius: 15px;
  font-size: 25px;
  font-weight: 700;
  text-align: center;
  margin: 0;
  padding: 3% 0;
}
.err {
  color: rgb(150, 45, 45);
  box-shadow: 0px 0px 2px 1px rgb(150, 45, 45);
}
.ok {
  color: #52c898;
  box-shadow: 0px 0px 2px 1px #52c898;
}
.invalid {
  border: 1px rgb(150, 45, 45) solid;
}
.error {
  position: absolute;
  color: rgb(150, 45, 45);
  left: 50%;
  bottom: -35%;
  font-size: 14px;
}
@media (max-width: 900px) {
  * {
    font-size: 20px;
  }
  .create-client {
    max-width: 900px;
  }
  .address,
  .basic,
  .document {
    display: grid;
    grid-template-columns: 1fr;
  }
  .input {
    flex-direction: column;
    &__input
    
     {
      height: 40px;
    }
    &__select
     {
      height: 60px;
    }
  }
  .submit {
    padding: 5%;
    margin-top: 5%;
  }
  .modal {
    top: 88%;
    right: 4%;
    padding: 5%;
  }
  .error {
    left: 2%;
    bottom: -25%;
  }
}
</style>
