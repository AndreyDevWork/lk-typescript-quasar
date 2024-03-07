<template>
  <q-layout view="hHh lpR lFf">
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title>Currency Converter</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container class="q-mx-auto container">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts"></script>
<style lang="scss" scoped>
.container {
  max-width: 1560px;
}
</style>
