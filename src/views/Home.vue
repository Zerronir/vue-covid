<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <CountrySelect @get-country="getCountry" :countries="countries" />
    <DataBoxes :stats="stats" />

    <button @click="clearCountryData" v-if="stats.Country"
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">Clear Country Data</button>

  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-grey-500 text-3xl mt-10 mb-6">
      <h1>Fetching Data</h1>
      <img :src="loadingImage" class="w-24 m-auto" />
    </div>

    

  </main>

</template>

<script>
import DataTitle from "@/components/DataTitle"
import DataBoxes from "@/components/DataBoxes"
import CountrySelect from "@/components/CountrySelect"

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data(){
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary');

      const data = await res.json();
      return data;
    },
    getCountry(item) {
      this.stats = item;
      this.title = item.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = 'Global';
      this.stats = data.Global;
      this.loading = false;
    }
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  }
}
</script>
