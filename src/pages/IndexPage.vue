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
      <q-btn
        v-if="!isSuccessLogin"
        @click="login"
        class="q-mt-md btn"
        color="primary"
        label="Войти"
      />
      <q-btn v-if="errorMessageLogin" class="q-mt-sm btn" color="negative">
        {{ errorMessageLogin }}
      </q-btn>
      <q-btn v-if="isSuccessLogin" class="q-mt-sm btn" color="positive">
        Аутентификация прошла успешно
      </q-btn>
    </div>
  </div>
</template>

<script setup lang="js">
import { reactive, ref } from 'vue'
import { httpClient } from 'src/services/httpClient'
import { useRouter } from 'vue-router'

const router = useRouter()

const signupForm = reactive({
  username: '',
  password: '',
})

const loginForm = reactive({
  grant_type: 'password',
  client_id: import.meta.env.VITE_AUTH_CLIENT_ID,
  client_secret: import.meta.env.VITE_AUTH_CLIENT_SECRET,
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
      errorMessage.value = ''
    })
    .catch((error) => {
      errorMessage.value = error.response.data.message
    })
}

const isSuccessLogin = ref(false)
const errorMessageLogin = ref('')
const login = () => {
  httpClient
    .post('oauth/token', loginForm)
    .then((response) => {
      isSuccessLogin.value = true
      errorMessageLogin.value = ''
      localStorage.setItem('ACCESS_TOKEN', response.data.access_token)
      router.push({ path: '/converter' })
    })
    .catch((error) => {
      console.log(error)
      errorMessageLogin.value = error.response.data.message
    })
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
