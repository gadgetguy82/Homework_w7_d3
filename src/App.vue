<template lang="html">

  <div class="whole-app">
    <h1>Countries of the World</h1>
    <div class="main-container">
      <div class="sub-container">
        <country-search :countryNames="countries.map(country => country.name)"></country-search>
        <country-select :countries="countries"></country-select>
      </div>
      <country-detail :country="selectedCountry"></country-detail>
      <!-- <countries-list :countries="countries"></countries-list> -->
    </div>
  </div>
</template>


<script>
import {eventBus} from "./main.js"
import CountryDetail from "./components/CountryDetail.vue"
import CountriesList from "./components/CountriesList.vue"
import CountrySelect from "./components/CountrySelect.vue"
import CountrySearch from "./components/CountrySearch.vue"

export default {
  name: "app",
  data() {
    return {
      countries: [],
      selectedCountry: null
    }
  },
  mounted(){
    fetch("https://restcountries.eu/rest/v2/all")
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on("country-selected", (countrySelected) => {
      this.selectedCountry = this.countries.find(country => country.name === countrySelected);
    })
  },
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail,
    "country-select": CountrySelect,
    "country-search": CountrySearch
  }
}
</script>

<style lang="css" scoped>
h1 {
  text-align: center;
  font-family: 'Bowlby One SC', cursive;
}

.whole-app {
  height: 580px;
}

.main-container {
  display: flex;
}
</style>
