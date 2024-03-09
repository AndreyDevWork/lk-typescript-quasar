<template>
  <q-layout view="hHh lpR lFf">
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title>
          <div class="flex justify-between">
            Currency Converter
            <q-btn
              @click="logout"
              color="white"
              text-color="black"
              label="Log out"
            />
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container class="q-mx-auto container">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { useRouter } from 'vue-router'

const router = useRouter()

const logout = () => {
  localStorage.removeItem('ACCESS_TOKEN')
  router.push('/')
}
</script>
<style lang="scss" scoped>
.container {
  max-width: 1560px;
}
</style>
