<template>
  <div class="client-form">
    <form @submit.prevent="submitForm" class="form">
      <!-- Фамилия -->
      <div class="form-group">
        <label for="surname">Фамилия*</label>
        <input type="text" id="surname" v-model="formData.surname" required />
        <span class="error-message">{{ formErrors.surname }}</span>
      </div>
      <!-- Имя -->
      <div class="form-group">
        <label for="name">Имя*</label>
        <input type="text" id="name" v-model="formData.name" required />
        <span class="error-message">{{ formErrors.name }}</span>
      </div>
      <!-- Отчество -->
      <div class="form-group">
        <label for="patronymic">Отчество</label>
        <input type="text" id="patronymic" v-model="formData.patronymic" />
      </div>
      <!-- Дата рождения -->
      <div class="form-group">
        <label for="dob">Дата рождения*</label>
        <input type="date" id="dob" v-model="formData.dob" required />
        <span class="error-message">{{ formErrors.dob }}</span>
      </div>
      <!-- Номер телефона -->
      <div class="form-group">
        <label for="phone">Номер телефона*</label>
        <input
          type="tel"
          id="phone"
          v-model="formData.phone"
          required
          pattern="[7]{1}[0-9]{10}"
        />
        <span class="error-message">{{ formErrors.phone }}</span>
      </div>
      <!-- Пол -->
      <div class="form-group">
        <label for="gender">Пол</label>
        <select id="gender" v-model="formData.gender">
          <option value="male">Мужской</option>
          <option value="female">Женский</option>
        </select>
      </div>
      <!-- Группа клиентов -->
      <div class="form-group">
        <label for="clientGroup">Группа клиентов*</label>
        <select
          id="clientGroup"
          v-model="formData.clientGroup"
          multiple
          required
        >
          <option value="VIP">VIP</option>
          <option value="problematic">Проблемные</option>
          <option value="OMS">ОМС</option>
        </select>
      </div>
      <!-- Лечащий врач -->
      <div class="form-group">
        <label for="doctor">Лечащий врач</label>
        <select id="doctor" v-model="formData.doctor">
          <option value="Ivanov">Иванов</option>
          <option value="Zaharov">Захаров</option>
          <option value="Chernysheva">Чернышева</option>
        </select>
      </div>
      <!-- Не отправлять СМС -->
      <div class="form-group">
        <label for="noSMS">Не отправлять СМС</label>
        <input type="checkbox" id="noSMS" v-model="formData.noSMS" />
      </div>

      <!-- Адрес -->
      <div class="section">
        <h3 class="section-title">Адрес</h3>
        <div class="section-content">
          <!-- Индекс -->
          <div class="form-group">
            <label for="index">Индекс</label>
            <input type="text" id="index" v-model="formData.address.index" />
          </div>
          <!-- Страна -->
          <div class="form-group">
            <label for="country">Страна</label>
            <input
              type="text"
              id="country"
              v-model="formData.address.country"
            />
          </div>
          <!-- Область -->
          <div class="form-group">
            <label for="region">Область</label>
            <input type="text" id="region" v-model="formData.address.region" />
          </div>
          <!-- Город -->
          <div class="form-group">
            <label for="city">Город*</label>
            <input
              type="text"
              id="city"
              v-model="formData.address.city"
              required
            />
            <span class="error-message">{{ formErrors.city }}</span>
          </div>
          <!-- Улица -->
          <div class="form-group">
            <label for="street">Улица</label>
            <input type="text" id="street" v-model="formData.address.street" />
          </div>
          <!-- Дом -->
          <div class="form-group">
            <label for="house">Дом</label>
            <input type="text" id="house" v-model="formData.address.house" />
          </div>
        </div>
      </div>

      <!-- Паспорт -->
      <div class="section">
        <h3 class="section-title">Паспорт</h3>
        <div class="section-content">
          <!-- Тип документа -->
          <div class="form-group">
            <label for="documentType">Тип документа*</label>
            <select
              id="documentType"
              v-model="formData.passport.documentType"
              required
            >
              <option value="passport">Паспорт</option>
              <option value="birthCertificate">Свидетельство о рождении</option>
              <option value="driverLicense">Вод. удостоверение</option>
            </select>
          </div>
          <!-- Серия -->
          <div class="form-group">
            <label for="series">Серия</label>
            <input type="text" id="series" v-model="formData.passport.series" />
          </div>
          <!-- Номер -->
          <div class="form-group">
            <label for="passportNumber">Номер*</label>
            <input
              type="text"
              id="passportNumber"
              v-model="formData.passport.number"
              required
            />
            <span class="error-message">{{ formErrors.passportNumber }}</span>
          </div>
          <!-- Кем выдан -->
          <div class="form-group">
            <label for="issuedBy">Кем выдан</label>
            <input
              type="text"
              id="issuedBy"
              v-model="formData.passport.issuedBy"
            />
          </div>
          <!-- Дата выдачи -->
          <div class="form-group">
            <label for="issueDate">Дата выдачи*</label>
            <input
              type="date"
              id="issueDate"
              v-model="formData.passport.issueDate"
              required
            />
            <span class="error-message">{{ formErrors.issueDate }}</span>
          </div>
        </div>
      </div>

      <button type="submit" class="submit-button">Создать клиента</button>
    </form>

    <div v-if="successMessage" class="success-message">
      {{ successMessage }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        surname: '',
        name: '',
        patronymic: '',
        dob: '',
        phone: '',
        gender: '',
        clientGroup: [],
        doctor: '',
        noSMS: false,
        address: {
          index: '',
          country: '',
          region: '',
          city: '',
          street: '',
          house: '',
        },
        passport: {
          documentType: '',
          series: '',
          number: '',
          issuedBy: '',
          issueDate: '',
        },
      },
      formErrors: {
        surname: '',
        name: '',
        dob: '',
        phone: '',
        city: '',
        passportNumber: '',
        issueDate: '',
      },
      successMessage: '',
    }
  },
  methods: {
    submitForm() {
      this.validateForm()

      if (Object.values(this.formErrors).every((error) => !error)) {
        this.successMessage = 'Новый клиент успешно создан!'

        this.clearForm()
      }
    },
    validateForm() {
      // Валидация Фамилии
      if (!this.formData.surname) {
        this.formErrors.surname = 'Введите фамилию'
      } else {
        this.formErrors.surname = ''
      }

      // Валидация Имени
      if (!this.formData.name) {
        this.formErrors.name = 'Введите имя'
      } else {
        this.formErrors.name = ''
      }

      // Валидация Даты рождения
      if (!this.formData.dob) {
        this.formErrors.dob = 'Введите дату рождения'
      } else {
        this.formErrors.dob = ''
      }

      // Валидация Номера телефона
      if (!this.formData.phone) {
        this.formErrors.phone = 'Введите номер телефона'
      } else if (!/^[7]{1}[0-9]{10}$/.test(this.formData.phone)) {
        this.formErrors.phone = 'Неверный формат номера телефона'
      } else {
        this.formErrors.phone = ''
      }

      // Валидация Города
      if (!this.formData.address.city) {
        this.formErrors.city = 'Введите город'
      } else {
        this.formErrors.city = ''
      }

      // Валидация Номера паспорта
      if (!this.formData.passport.number) {
        this.formErrors.passportNumber = 'Введите номер паспорта'
      } else {
        this.formErrors.passportNumber = ''
      }

      // Валидация Даты выдачи паспорта
      if (!this.formData.passport.issueDate) {
        this.formErrors.issueDate = 'Введите дату выдачи паспорта'
      } else {
        this.formErrors.issueDate = ''
      }
    },
    clearForm() {
      // Очистка формы
      this.formData = {
        surname: '',
        name: '',
        patronymic: '',
        dob: '',
        phone: '',
        gender: '',
        clientGroup: [],
        doctor: '',
        noSMS: false,
        address: {
          index: '',
          country: '',
          region: '',
          city: '',
          street: '',
          house: '',
        },
        passport: {
          documentType: '',
          series: '',
          number: '',
          issuedBy: '',
          issueDate: '',
        },
      }
      this.successMessage = ''
    },
  },
}
</script>

<style scoped>
.client-form {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 20px;
}

input[type='text'],
input[type='tel'],
input[type='date'],
select {
  width: calc(100% - 24px);
  padding: 10px;
  margin-right: 12px;
  border: 1px solid #ccc;
  border-radius: 5px;
  transition: border-color 0.3s ease;
}

input[type='text']:focus,
input[type='tel']:focus,
input[type='date']:focus,
select:focus {
  border-color: #66afe9;
  outline: none;
}

.submit-button {
  background-color: #4caf50;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #45a049;
}

.success-message {
  margin-top: 20px;
  color: green;
}

.error-message {
  color: red;
  font-size: 14px;
  margin-top: 5px;
}
</style>
