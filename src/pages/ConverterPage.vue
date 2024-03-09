<template>
  <div class="q-mx-auto q-pt-md wrapper">
    <CurrenciesTable v-if="currencyies.length" :currencyies="currencyies" />
  </div>
</template>

<script setup>
import CurrenciesTable from 'components/CurrenciesTable.vue'
import { ref } from 'vue'
import { httpClient } from 'src/services/httpClient.js'
import { useRouter } from 'vue-router'

const currencyies = ref([])
const router = useRouter()

const headers = {
  Authorization: `Bearer ${localStorage.getItem('ACCESS_TOKEN')}`,
}
const getCurrencyies = () => {
  currencyies.value = httpClient
    .get('/api/currency', { headers })
    .then((response) => {
      currencyies.value = response.data
    })
    .catch((error) => {
      if (error.response && error.response.status === 401) {
        localStorage.removeItem('ACCESS_TOKEN')
        router.push('/')
      }
    })
}
getCurrencyies()
</script>

<style lang="scss" scoped>
.wrapper {
  width: fit-content;
}
</style>
