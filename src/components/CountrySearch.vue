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
  .autocomplete {
    position: relative;
    display: inline-block;
  }

  .autocomplete-items {
    position: absolute;
    border: 1px solid #d4d4d4;
    border-bottom: none;
    border-top: none;
    z-index: 99;
    /*position the autocomplete items to be the same width as the container:*/
    top: 100%;
    left: 0;
    right: 0;
  }

  .autocomplete-items div {
    padding: 10px;
    cursor: pointer;
    background-color: #fff;
    border-bottom: 1px solid #d4d4d4;
  }

  .autocomplete-items div:hover {
    /*when hovering an item:*/
    background-color: #e9e9e9;
  }

  .autocomplete-active {
    /*when navigating through the items using the arrow keys:*/
    background-color: DodgerBlue !important;
    color: #ffffff;
  }
  </style>
