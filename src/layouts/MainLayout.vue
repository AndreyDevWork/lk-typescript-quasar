<template>
  <q-layout view="lHh lpr lFf">
    <q-drawer :breakpoint="1047" class="bg-purple" show-if-above>
      <div class="logo q-px-md flex items-center">
        <AppLogo />
      </div>
    </q-drawer>

    <q-header class="flex items-center header">
      <div class="humburger cursor-pointer column flex-center">
        <span></span>
        <span></span>
        <span></span>
      </div>
      <AppLogo class="header-logo" />
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import AppLogo from 'components/icons/AppLogo.vue'
</script>

<style lang="scss" scoped>
.humburger {
  span {
    display: block;
    height: 2px;
    width: 20px;
    border-radius: 4px;
    background: $purple-2;
  }
}
.logo {
  height: 72px;
  border-bottom: 1px solid $purple-1;
}
.header {
  height: 72px;
  background: white;
}
.humburger {
  width: 56px;
  height: 56px;
  border-right: 1px solid $purple-1;
  row-gap: 4px;
  display: none;
}
.header-logo {
  visibility: hidden;
}

@media (max-width: $breakpoint-md-min) {
  .header {
    background: $purple;
    height: 56px;
    column-gap: 16px;
  }
  .humburger {
    display: flex;
  }
  .header-logo {
    visibility: visible;
    width: 126px;
  }
}
</style>
