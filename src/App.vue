<template>
  <div id="app">

    <div class="fullForm">

      <div class="menu_cross">
        <span class="invisible_text">Н</span>
        <span class="menu_name">Заявка на карту</span>
        <button
          class="cross"
          style="background-image: url(/img/close_white.png);"
          @click="closeForm"
        ></button>
      </div>
      <form class="menu" @submit.prevent="submitForm" autocomplete="off">
        <div class="inputs">
          <div class="form-group">
            <input
              class="input"
              placeholder="ФИО"
              v-model.trim="form.name"
              id="name"
              :class="isNameValid"
            />
            <p v-show="form.name && !isNameValid" class="error-message">Некорректно введены данные</p>
          </div>

          <div class="form-group">
            <input
              class="input"
              placeholder="Электронный адрес"
              v-model.trim="form.email"
              id="email"
              :class="isEmailValid"
            />
            <p v-show="form.email && !isEmailValid" class="error-message">Некорректно введены данные</p>
          </div>

          <div class="form-group">
            <input
              class="input"
              type="tel"
              placeholder="Номер телефона"
              v-model.number="form.phone"
              id="phone"
              :class="isPhoneValid"
            />
            <p v-show="form.phone && !isPhoneValid" class="error-message">Некорректно введены данные</p>
          </div>

          <div class="form-group">
            <select name="country" id="country" v-model="form.country">
              <option class="country_choose" selected>Российская Федерация</option>
              <option class="country_choose">Белорусь</option>
              <option class="country_choose">Украина</option>
              <option class="country_choose">Казахстан</option>
            </select>
          </div>

          <input type="checkbox" id="checkbox" required />
          <label class="checkbox_text">
            Я соглашаюсь на
            <span class="checkbox_text_white_word">обработку</span>
            моих персональных данных
          </label>
        </div>

        <div>
          <button
            class="submit"
            @click="sendForm"
            :disabled="!formIsValid"
            :class="{ '-valid': formIsValid }"
          >Заказать сейчас</button>
        </div>
      </form>


    </div>


    <div class="message" @click="closeForm">
      <div class="message_center">
      <div class="message_img">
      <img class="img" src="/img/ok.png" alt="">
      </div>
      <p class="message_main_text">Ваша заявка принята</p>
      <p class="message_subtext">В ближайшее время с вами свяжется наш менеджер</p>
      </div>
    </div>


  </div>

</template>










<script>
export default {
  name: "app",
  data() {
    return {
      form: {
        name: "",
        email: "",
        phone: "",
        country: null
      }
    };
  },

  computed: {
    isPhoneValid() {
      return /^(\s*)?(\+)?([- _():=+]?\d[- _():=+]?){10,14}(\s*)?$/.test(
        this.form.phone
      );
    },
    isNameValid() {
      return /^([А-ЯA-Z]|[А-ЯA-Z][\x27а-яa-z]{1,}|[А-ЯA-Z][\x27а-яa-z]{1,}\-([А-ЯA-Z][\x27а-яa-z]{1,}|(оглы)|(кызы)))\040[А-ЯA-Z][\x27а-яa-z]{1,}(\040[А-ЯA-Z][\x27а-яa-z]{1,})?$/.test(
        this.form.name
      );
    },
    isEmailValid() {
      return /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
        this.form.email
      );
    },
    formIsValid() {
      return this.isPhoneValid && this.isNameValid && this.isEmailValid;
    }
  },

  methods: {
    closeForm: function() {
      document.getElementById("app").style.display = "none";
      document.getElementById("main").style.display = "block";
      document.getElementById("app").getElementsByClassName("fullForm")[0].style.display = "block";
      document.getElementById("app").getElementsByClassName("message")[0].style.display = "none";
      this.form = {
        name: "",
        email: "",
        phone: "",
        country: null
      };
    },

     sendForm: function() {
      document.getElementById("app").getElementsByClassName("fullForm")[0].style.display = "none";
      document.getElementById("app").getElementsByClassName("message")[0].style.display = "block";
      this.form = {
        name: "",
        email: "",
        phone: "",
        country: null
      };
    },

    submitForm() {
      if (this.formIsValid) {
        console.log("Form Submitted", this.form);
      } else {
        console.log("Invalid form");
      }
    }
  }
};
</script>









<style lang="scss">
#app {
  z-index: 99999;
  width: 100%;
  height: 100%;
  background: #000000;
  display: none;
}

.fullForm {
  height: 100%;
}

.menu {
  padding-top: 1.5%;
  margin: 0 auto;
  width: 35.416667%;
  align-items: center;
  padding-bottom: 12%;
}

.form-group {
  padding-top: 20px;
}

.menu_name {
  margin: 0 auto;
  width: 253px;
  height: 34px;
  font-style: normal;
  font-weight: 800;
  font-size: 30px;
  line-height: 113.22%;
  text-align: center;
  padding-bottom: 80px;
}

.input {
  width: 680px;
  height: 80px;
  border-radius: 10px;
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 113.22%;
  background-color: #6c6c6c;
  border-color: #6c6c6c;
  color: white;
  padding-left: 30px;
}

::-webkit-input-placeholder {
  color: white;
}

select {
  width: 680px;
  height: 80px;
  border-radius: 10px;
  font-style: normal;
  font-weight: 500;
  background-color: #6c6c6c;
  font-size: 20px;
  line-height: 113.22%;
  border-color: #6c6c6c;
}

#country {
  width: 680px;
  padding-left: 30px;
  color: white;
}

.country_choose {
  width: 680px;
  height: 80px;
  border-radius: 10px;
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 113.22%;
  background-color: #6c6c6c;
  color: #ffffff;
}

#checkbox {
  margin-top: 25px;
  width: 39px;
  height: 39px;
  border-radius: 10px;
  background: #191919;
}

.submit {
  background: #6c6c6c;
  border-color: #6c6c6c;
  border-radius: 10px;
  width: 290px;
  height: 80px;
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  margin-top: 25px;
  color: #ffffff;
}

.submit.-valid {
  background: #c0965c;
  border-color: #c0965c;
}

.checkbox_text {
  width: 458px;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  color: #6c6c6c;
  padding-left: 20px;
}

.checkbox_text_white_word {
  color: #bbbbbb;
}

.error-message {
  padding-top: 15px;
  padding-left: 30px;
  font-style: normal;
  font-weight: 500;
  font-size: 12px;
  line-height: 113.22%;
  color: #cc301b;
}

.cross {
  height: 48px;
  width: 48px;
  background-color: black;
  border: black;
}

.menu_cross {
  width: 35.416667%;
  margin: 0 auto;
  padding-top: 5%;
  font-style: normal;
  font-weight: 800;
  font-size: 30px;
  line-height: 113.22%;
  color: #ffffff;
  text-align: center;
  display: flex;
  flex-direction: row;
}

.invisible_text {
  color: black;
}


.message {
  margin: 0 auto;
  width: 22%;
  height: 100vh;
  display: none;
}

.message_img{
  width: 10%;
  margin: 0 auto;
  align-items: center;
}

.message_main_text {
  padding-top: 19px;
  font-style: normal;
  font-weight: 800;
  font-size: 30px;
  line-height: 113.22%;
  text-align: center;
  color: #FFFFFF;
}

.message_subtext {
  padding-top: 12px;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  color: #6C6C6C;
}

.message_center {
  padding-top: 80%;
}

</style>
