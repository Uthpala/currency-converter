<template>
  <div class="mt-6">
    <div>
      <input
        v-model.number="sourceAmount"
        type="text"
        class="shadow-sm focus:ring-blue-500 focus:border-blue-500 sm:text-sm border-gray-300 rounded-md"
      />
      <select
        id="sourceCurrency"
        v-model="sourceCurrency"
        name="sourceCurrency"
        class="ml-2 pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm rounded-md"
      >
        <option
          v-for="currencySymbol in Object.keys(currencies.rates)"
          :key="currencySymbol"
        >
          {{ currencySymbol }}
        </option>
      </select>
    </div>
    <div class="mt-4">
      <button
        type="button"
        class="inline-flex my-2 items-center px-4 py-2 border border-gray-300 shadow-sm text-sm rounded-md text-gray-700 bg-gray-50 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-blue-500"
        @click="targets.push(Date.now())"
      >
        Convert to more currencies
      </button>
      <TargetCurrency
        v-for="target in targets"
        :key="target"
        :rates="currencies.rates"
        :source-amount="sourceAmount"
        :source-currency="sourceCurrency"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currencies: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      sourceAmount: 1,
      sourceCurrency: 'GBP',
      targets: [Date.now()],
    }
  },
}
</script>
