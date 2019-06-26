<template lang="html">
  <div class="search-container">
    <div class="search">
      <input type="text" v-on:input="handleInput" v-model="search" placeholder="Search a country">
    </div>
    <div class="autocomplete" v-if="autocompleteList !== []">
      <countries-list :countries="autocompleteList"></countries-list>
    </div>
  </div>
</template>

<script>
import {eventBus} from "../main.js"
import CountriesList from "./CountriesList.vue"

export default {
  name: "country-search",
  data() {
    return {
      search: "",
      autocompleteList: []
    }
  },
  props: ["countryNames"],
  methods: {
    autocompleteFilter() {
      const filteredCountries = this.countryNames.filter(
        name => name.substr(0, this.search.length).toLowerCase() === this.search.toLowerCase()
      );
      return filteredCountries.length === this.countryNames.length ? [] : filteredCountries;
    },
    handleInput() {
      this.autocompleteList = this.autocompleteFilter();
      // eventBus.$emit("autocomplete-list", this.autocompleteList);
    }
  },
  components: {
    "countries-list": CountriesList,
  }
}
</script>

<style lang="css" scoped>
input {
  font-size: 16px;
  width: 100%;
  padding: 0;
}

.search-container {
  width: 100%;
}

.search {
  margin: 0;
  padding: 0;
}

.autocomplete {
  position: relative;
  margin: 0;
  padding: 0;
}
</style>
