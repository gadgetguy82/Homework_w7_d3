<template lang="html">
  <div v-if="countries">
    <select v-on:change="handleChange" v-model="countrySelected">
      <option value="" disabled>Select a country</option>
      <list-item v-for="(country, index) in countries" :country="country" :key="index"></list-item>
    </select>
  </div>
</template>

<script>
import ListItem from "./ListItem.vue"
import {eventBus} from "../main.js"

export default {
  name: "countries-list",
  data() {
    return {
      countrySelected: ""
    }
  },
  props: ["countries"],
  components: {
    "list-item": ListItem
  },
  methods: {
    handleChange() {
      eventBus.$emit("country-selected", this.countries.find(country => country.name === this.countrySelected));
    }
  }
}
</script>

<style lang="css" scoped>
</style>
