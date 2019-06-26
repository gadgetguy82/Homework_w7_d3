<template lang="html">
  <div class="list" v-if="countries">
    <select v-on:change="handleChange" v-model="countrySelected">
      <option value="" disabled>Select a country</option>
      <option v-for="(country, index) in countries" :key="index">{{country.name}}</option>
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
      eventBus.$emit("country-selected", this.countrySelected);
    }
  }
}
</script>

<style lang="css" scoped>
select {
  font-size: 16px;
}

.list {
  margin-top: 10px;
}
</style>
