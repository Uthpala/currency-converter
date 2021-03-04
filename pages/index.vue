<template>
  <div class="container mx-auto p-4">
    <client-only>
      <div class="flex py-4 border-b">
        <p class="font-medium py-1 mr-8">Currency rates on</p>
        <date-picker
          v-model="selectedDate"
          value-type="format"
          :disabled-date="disabledDates"
          @input="fetchCurrencyData"
        />
      </div>
    </client-only>
    <CurrencyConverter v-if="currencies" :currencies="currencies" />
  </div>
</template>

<script>
import { format } from 'date-fns'
import 'vue2-datepicker/index.css'

export default {
  name: 'Home',
  data() {
    return {
      selectedDate: format(new Date(), 'yyyy-MM-dd'),
      currencies: null,
    }
  },
  mounted() {
    this.fetchCurrencyData()
  },
  methods: {
    fetchCurrencyData() {
      this.$axios
        .$get(`https://api.exchangeratesapi.io/${this.selectedDate}`)
        .then((res) => {
          this.currencies = res
        })
    },
    disabledDates(date) {
      const dataAvailableSinceYear = 1999
      return date.getFullYear() < dataAvailableSinceYear || date > new Date()
    },
  },
}
</script>
