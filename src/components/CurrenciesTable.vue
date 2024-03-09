<template>
  <div class="q-pa-md">
    <q-table
      v-if="currencyies.length"
      title="Currencyies"
      :rows="props.currencyies"
      :columns="columns"
      row-key="name"
      rows-per-page-options="0"
    />
  </div>
</template>

<script setup>
const props = defineProps(['currencyies'])

const columns = [
  {
    label: 'Name',
    field: 'name',
    align: 'left',
  },
  {
    label: 'CHAR CODE',
    field: 'char_code',
    align: 'left',
  },
  {
    label: 'NOMINAL',
    field: 'nominal',
    align: 'left',
  },
  {
    label: 'VALUE',
    field: 'value',
    align: 'left',
  },
  {
    label: 'VUNIT RATE',
    field: 'vunit_rate',
    align: 'left',
  },
  {
    label: 'UPDATED AT',
    field: 'updated_at',
    align: 'left',
  },
]
</script>
