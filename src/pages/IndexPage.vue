<template>
  <div class="q-mx-auto q-pt-md wrapper">
    <div class="register">
      <div class="title">Sign-up</div>
      <q-input v-model="text" label="Standard" />
    </div>
  </div>
</template>

<script setup lang="ts"></script>
<style lang="scss" scoped>
.wrapper {
  width: fit-content;
}
.title {
  font-size: 30px;
  font-weight: 500;
  text-align: center;
}
</style>
