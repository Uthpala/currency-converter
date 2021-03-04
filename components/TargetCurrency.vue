<template>
  <div class="flex mt-3">
    <p class="px-4 py-2 border rounded-md mr-2 w-40">
      {{ targetAmount }}
    </p>
    <select
      id="targetCurrency"
      v-model="targetCurrency"
      name="targetCurrency"
      class="block w-32 pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md"
      @change="$emit('change', targetCurrency)"
    >
      <option
        v-for="currencySymbol in Object.keys(rates)"
        :key="currencySymbol"
      >
        {{ currencySymbol }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'TargetCurrency',
  props: {
    rates: {
      type: Object,
      required: true,
    },
    sourceAmount: {
      type: Number,
      required: true,
    },
    sourceCurrency: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      targetCurrency: 'USD',
    }
  },
  computed: {
    targetAmount() {
      return (
        (parseFloat(this.sourceAmount) / this.rates[this.sourceCurrency]) *
        this.rates[this.targetCurrency]
      ).toFixed(2)
    },
  },
}
</script>
