<template>
  <div class="q-pa-md">
    <q-card class="my-card">
      <q-card-section>
        <div class="text-h6">Converter</div>
        <div
          class="text-subtitle2"
        >
          Конвертация ведётся в расчётах на НОМИНАЛ
        </div>
        <div style="column-gap: 10px" class="q-mt-md flex">
          <q-select
            filled
            square
            v-model="firstSelect"
            use-input
            hide-selected
            fill-input
            input-debounce="0"
            label="Currency"
            :options="options"
            @filter="filterFn"
            behavior="menu"
          >
            <template v-slot:no-option>
              <q-item>
                <q-item-section class="text-grey"> No results </q-item-section>
              </q-item>
            </template>
          </q-select>

          <q-input
            type="number"
            square
            filled
            label="Sum"
            v-model="firstValue"
          />
          <div
            v-if="conversionRateFirst"
            class="items-center flex text-subtitle1">
            NOMINAL = X {{ conversionRateFirst.nominal }}
          </div>
        </div>

        <div style="column-gap: 10px" class="q-mt-md flex">
          <q-select
            filled
            square
            v-model="secondSelect"
            use-input
            hide-selected
            fill-input
            input-debounce="0"
            label="Currency"
            :options="options"
            @filter="filterFn"
            behavior="menu"
          >
            <template v-slot:no-option>
              <q-item>
                <q-item-section class="text-grey"> No results </q-item-section>
              </q-item>
            </template>
          </q-select>

          <q-input
            square
            type="number"
            filled
            v-model="secondValue"
            label="Sum"
          />
          <div
            v-if="conversionRateSecond"
            class="items-center flex text-subtitle1">
            NOMINAL = X {{ conversionRateSecond.nominal }}
          </div>
        </div>
      </q-card-section>
    </q-card>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const firstSelect = ref(null)
const firstValue = ref(null)

const secondSelect = ref(null)
const secondValue = ref(null)

const props = defineProps(['currencyies'])
const stringOptions = props.currencyies.map((item) => item.char_code)

const options = ref(stringOptions)
const filterFn = (val, update) => {
  if (val === '') {
    update(() => {
      options.value = stringOptions
    })
    return
  }

  update(() => {
    const needle = val.toLowerCase()
    options.value = stringOptions.filter(
      (v) => v.toLowerCase().indexOf(needle) > -1,
    )
  })
}

const conversionRateFirst = computed(() => {
  const selectedCharCode = firstSelect.value
  if (selectedCharCode) {
    const selectedCurrency = props.currencyies.find(
      (currency) => currency.char_code === selectedCharCode,
    )
    return selectedCurrency || null
  }
  return null
})
const conversionRateSecond = computed(() => {
  const selectedCharCode = secondSelect.value
  if (selectedCharCode) {
    const selectedCurrency = props.currencyies.find(
      (currency) => currency.char_code === selectedCharCode,
    )
    return selectedCurrency || null
  }
  return null
})

const convertFirst = () => {
  if (firstSelect.value && secondSelect.value) {
    const res = (secondValue.value / conversionRateFirst.value.value) * conversionRateSecond.value.value
    firstValue.value = res.toFixed(4)
  }
}

const convertSecond = () => {
  if (firstSelect.value && secondSelect.value) {
    const res = (firstValue.value / conversionRateSecond.value.value) * conversionRateFirst.value.value
    secondValue.value = res.toFixed(4)
  }
}

watch(secondValue, () => {
  convertFirst()
})
watch(firstValue, () => {
  convertSecond()
})

watch(firstSelect, () => {
  secondValue.value = 0
})

watch(secondSelect, () => {
  firstValue.value = 0
})

</script>

<style lang="scss">
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  /* display: none; <- Crashes Chrome on hover */
  -webkit-appearance: none;
  margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
}
</style>
