<template>
  <div class="form">
    <div class="form__container">
      <h1 class="form__title">Регистрация</h1>
      <p class="form__subtitle">
        Уже есть аккаунт? <a class="form__link">Войти</a>
      </p>
      <form @submit.prevent="submit">
        <div class="form__input">
          <label for="name" class="form__label">Имя</label>
          <input
            class="form__input-field"
            type="text"
            name="name"
            placeholder="Введите Ваше имя"
            required
            v-model="name"
          />
          <p class="form__error">{{ errors.name }}</p>
        </div>
        <div class="form__input">
          <label for="email" class="form__label">Email</label>
          <input
            class="form__input-field"
            type="text"
            name="email"
            placeholder="Введите Ваш email"
            required
            v-model="email"
          />
          <p class="form__error">{{ errors.email }}</p>
        </div>
        <div class="form__input">
          <label for="name" class="form__label">Номер телефона</label>
          <input
            class="form__input-field"
            type="text"
            name="phone"
            placeholder="Введите номер телефона"
            required
            v-model="phone"
          />
          <p class="form__error">{{ errors.phone }}</p>
        </div>
        <div class="form__input">
          <label for="lang" class="form__label">Язык</label>
          <div class="form__select-wrapper">
            <input
              type="text"
              autocomplete="off"
              class="form__input-field form__select-field"
              name="lang"
              placeholder="Язык"
              required
              v-model="lang"
              @click="showLangOptions = true"
              @keypress.prevent=""
              @blur="closeOptions"
            />
            <ul class="form__select-options" v-show="showLangOptions">
              <li
                class="form__select-option"
                v-for="langOp in langOptions"
                :key="langOp"
                @click="
                  lang = langOp;
                  showLangOptions = false;
                  verifyForm();
                "
              >
                {{ langOp }}
              </li>
            </ul>
          </div>
        </div>
        <div class="form__rules">
          <label for="rules" class="form__rules-checkbox">
            <input
              type="checkbox"
              name="rules"
              v-model="rules"
              @change="verifyForm"
            />
            <span class="form__rules-checkmark"></span>
          </label>
          <span>Принимаю <a class="form__link">условия</a> использования </span>
        </div>
        <button type="submit" class="form__button" :disabled="buttonDisabled">
          Зарегистрироваться
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      phone: "",
      lang: "",
      langOptions: ["Русский", "Английский", "Китайский", "Испанский"],
      showLangOptions: false,
      rules: false,
      buttonDisabled: true,
      errors: {
        name: "",
        email: "",
        phone: "",
      },
    };
  },
  methods: {
    closeOptions() {
      setTimeout(() => (this.showLangOptions = false), 100);
    },
    verifyForm() {
      if (
        this.name &&
        this.email &&
        this.phone &&
        this.lang &&
        this.rules &&
        !this.errors.name &&
        !this.errors.email &&
        !this.errors.phone
      ) {
        this.buttonDisabled = false;
      } else {
        this.buttonDisabled = true;
      }
    },
    submit() {
      console.log("Форма заполнена без ошибок и готова к отправке на сервер");
    },
  },
  watch: {
    name: function () {
      if (this.name.match(/([A-Za-zА-Яа-я\s-])+/g)[0] !== this.name) {
        this.errors.name = "Может содержать только буквы, пробелы и дефис";
        this.verifyForm();
      } else {
        this.errors.name = "";
        this.verifyForm();
      }
    },
    email: function () {
      if (
        !this.email.match(
          /[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?/
        ) ||
        this.email.match(
          /[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?/
        )[0] !== this.email
      ) {
        this.errors.email = "Введено некорректное значение";
        this.verifyForm();
      } else {
        this.errors.email = "";
        this.verifyForm();
      }
    },
    phone: function () {
      if (
        !this.phone.match(/\+\d\(\d{3}\)\d{3}-\d{2}-\d{2}/) ||
        this.phone.match(/\+\d\(\d{3}\)\d{3}-\d{2}-\d{2}/)[0] !== this.phone
      ) {
        this.errors.phone = "Должен быть в формате +7(123)456-78-90";
        this.verifyForm();
      } else {
        this.errors.phone = "";
        this.verifyForm();
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.form {
  &__container {
    margin: 50px 0;
    width: 460px;
    background-color: #fff;
    border-radius: 24px;
    box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02),
      0px 32px 64px rgba(44, 39, 56, 0.04);
    padding: 40px 30px;
  }

  &__title {
    margin: 0;
    font-weight: 700;
    font-size: 34px;
  }

  &__link {
    color: #0880ae;
    cursor: pointer;
    font-weight: 500;
  }

  &__subtitle {
    margin-bottom: 58px;
  }

  &__label {
    margin: 8px 0;
    display: block;
    color: #756f86;
  }

  &__input-field {
    width: 100%;
    border: 1px solid #dbe2ea;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    border-radius: 6px;
    padding: 16px;
    font-family: "IBM Plex Sans";
    font-size: 16px;
    &::placeholder {
      color: #7c9cbf;
    }
    &:focus {
      border: 2px solid #0880ae;
    }
  }

  &__error {
    min-height: 20px;
    margin: 8px 0;
    color: #ff7171;
    font-size: 14px;
  }

  &__select-field {
    caret-color: transparent;
    cursor: default;
  }

  &__select-wrapper {
    position: relative;
    &::before {
      border-style: solid;
      border-width: 2px 2px 0 0;
      content: "";
      display: inline-block;
      height: 12px;
      width: 12px;
      position: absolute;
      top: 20px;
      right: 16px;
      transform: rotate(135deg);
      vertical-align: top;
      color: #0880ae;
      z-index: 3;
    }
  }

  &__select-options {
    position: absolute;
    z-index: 5;
    left: 0;
    top: 60px;
    width: 100%;
    padding: 12px 0;
    background-color: #fff;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04),
      0px 20px 20px rgba(44, 39, 56, 0.04);
    border: 1px solid #dbe2ea;
    border-radius: 6px;
  }

  &__select-option {
    padding: 12px 16px;
    color: #756f86;
    &:hover {
      background-color: #ebf4f8;
    }
  }

  &__rules {
    display: flex;
    align-items: center;
    margin-top: 36px;
  }

  &__rules-checkbox {
    display: inline-block;
    width: 28px;
    height: 28px;
    position: relative;
    margin-right: 8px;

    & input {
      position: absolute;
      opacity: 0;
      height: 100%;
      width: 100%;
      cursor: pointer;
      z-index: 3;

      &:hover,
      &:focus {
        & ~ .form__rules-checkmark {
          border: 2px solid #0880ae;
          border-radius: 4px;
        }
      }
      &:checked {
        ~ .form__rules-checkmark {
          border-color: #0880ae;
          &::after {
            content: "";
            position: absolute;
            left: 4px;
            top: 0;
            width: 8px;
            height: 14px;
            border: solid #0880ae;
            margin: 4px;
            border-width: 0 2px 2px 0;
            transform: rotate(45deg);
          }
        }
      }
    }
  }

  &__rules-checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 28px;
    width: 28px;
    border: 2px solid #dbe2ea;
    border-radius: 4px;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  }

  &__button {
    width: 100%;
    height: 56px;
    margin-top: 40px;
    color: #ebf4f8;
    background-color: #0880ae;
    box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
      0px 4px 8px rgba(44, 39, 56, 0.08);
    border-radius: 6px;
    font-size: 16px;

    &:hover,
    &:focus {
      box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.08),
        0px 24px 48px rgba(44, 39, 56, 0.16);
    }

    &:active {
      border: 2px solid rgba(44, 39, 56, 0.86);
      box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.0001),
        0px 4px 8px rgba(44, 39, 56, 0.08);
    }

    &:disabled {
      background-color: #dbe2ea;
      color: rgba(44, 39, 56, 0.3);
      cursor: not-allowed;
      &:hover {
        box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
          0px 4px 8px rgba(44, 39, 56, 0.08);
      }
    }
  }
}

@media (max-width: 460px) {
  .form__container {
    width: 100%;
    margin: 10px 0;
  }
}
</style>