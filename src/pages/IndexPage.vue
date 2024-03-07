<template>
  <div class="q-mx-auto q-pt-md wrapper">
    <div class="left">
      <div class="form">
        <div class="title">Регистрация</div>
        <q-input v-model="signupForm.username" label="username" />
        <q-input v-model="signupForm.password" label="password" />
        <q-btn
          v-if="!isSuccess"
          @click="signup"
          class="q-mt-md btn"
          color="primary"
          label="Зарегестрироваться"
        />
        <q-btn v-if="errorMessage" class="q-mt-sm btn" color="negative">
          {{ errorMessage }}
        </q-btn>
        <q-btn v-if="isSuccess" class="q-mt-sm btn" color="positive">
          Вы успешно зарегестрировались
        </q-btn>
      </div>
    </div>
    <div class="right">
      <div class="title">Вход</div>
      <q-input v-model="loginForm.username" label="username" />
      <q-input v-model="loginForm.password" label="password" />
      <q-btn @click="login" class="q-mt-md btn" color="primary" label="Войти" />
    </div>
  </div>
</template>

<script setup lang="js">
import { reactive, ref } from 'vue'
import { httpClient } from 'src/services/httpClient'

const signupForm = reactive({
  username: '',
  password: '',
})

const loginForm = reactive({
  username: '',
  password: '',
})

const isSuccess = ref(false)
const errorMessage = ref('')

const signup = () => {
  httpClient
    .post('/api/auth/register', signupForm)
    .then(() => {
      isSuccess.value = true
      errorMessage.value = false
    })
    .catch((error) => {
      errorMessage.value = error.response.data.message
    })
}

const login = () => {
  console.log('войти')
}
</script>

<style lang="scss" scoped>
.wrapper {
  width: fit-content;
  display: grid;
  grid-template-columns: 340px 340px;
  column-gap: 40px;
}
.btn {
  width: 100%;
}
.form {
  width: 340px;
}
.title {
  font-size: 30px;
  font-weight: 500;
  text-align: center;
}
</style>
