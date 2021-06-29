<template>
  <div class="registration-form">
    <form @submit.prevent="handleSubmit" class="form-wrapper">
      <h2>VeeValidate Playground User Registration</h2>
      <input
        v-model="formData.name"
        v-validate.continues="'required|alpha_spaces|max:50'"
        name="full_name"
        type="text"
        placeholder="Full Name"
        class="text-field"
      />
      <p class="error-message">{{ errors.first('full_name') }}</p>
      <input
        v-model="formData.phoneNumber"
        v-validate="'required|numeric'"
        name="phone_number"
        type="text"
        placeholder="Phone Number"
        class="text-field"
      />
      <p class="error-message">{{ errors.first('phone_number') }}</p>
      <input
        v-model="formData.email"
        v-validate="'required|email'"
        name="email"
        type="email"
        placeholder="Email"
        class="text-field"
      />
      <p class="error-message">{{ errors.first('email') }}</p>
      <input
        v-model="formData.password"
        v-validate="'required|min:8'"
        name="password"
        type="password"
        placeholder="Password"
        ref="password"
        class="text-field"
      />
      <p class="error-message">{{ errors.first('password') }}</p>
      <input
        v-model="formData.confirmedPassword"
        v-validate="'required|confirmed:password'"
        name="password_confirmation"
        type="password"
        placeholder="Confirm Password"
        class="text-field"
      />
      <p class="error-message">
        {{ errors.first('password_confirmation') }}
      </p>
      <button>Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'RegistrationForm',
  data() {
    return {
      formData: {
        full_name: '',
        phoneNumber: '',
        email: '',
        password: '',
        confirmedPassword: ''
      }
    };
  },
  methods: {
    handleSubmit() {
      this.$validator.validateAll()
        .then(response => {
          alert(response ? 'Submitted!' : 'Form is dirty!')
        })
        .catch(error => { console.error(error) })
    }
  }
}
</script>

<style scoped>
button {
  margin-top: 24px;
  color: #4fc08d;
  cursor: pointer;
  width: 100%;
  background: none;
  border: solid 1px;
  border-radius: 8px;
  font: inherit;
  padding: 0.75em 2em;
}
  
.form-wrapper {
  max-width: 411px;
  padding: 24px;
  margin: 0 auto;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.text-field {
  width: 95.5%;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 8px;
  margin-top: 8px;
}

.error-message {
  margin-top: 8px;
  font-size: 12px;
  color: red;
}
</style>