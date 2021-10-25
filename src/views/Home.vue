<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />

    <CountrySelect @get-country="getCountryData" :countries="countries"/>

    <DataBoxes :stats="stats" />

    <button @click="clearCountryData" v-if="stats.Country" class="bg-blue-700 text-white rounded p-3 mb-10 mt-5 focus:outline-none hover:bg-blue-500">
      Clear Country
    </button>
  </main>

  <main v-else> still loading </main>
</template>

<script>
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'
import CountrySelect from '@/components/CountrySelect'

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: []
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    },
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData() {
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading = false
    }
  },
  async created(){
    const data = await this.fetchCovidData()
    
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  }
};
</script>
