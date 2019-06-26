<template lang="html">
  <div class="detail" v-if="country">
    <h3>{{country.name}}</h3>
    <p>Capital: {{country.capital}}</p>
    <p>Population: {{country.population}}</p><br>
    <span>Languages Spoken:</span>
    <ul>
      <li v-for="language in country.languages">{{language.name}}</li>
    </ul>
    <img :src="country.flag">
  </div>
</template>

<script>
export default {
  name: "country-detail",
  props: ["country"]
}
</script>

<style lang="css" scoped>
ul {
  margin: 0;
  padding: 20px;
  list-style: none;
}

img {
  height: 200px;
}

.detail {
  text-align: center;
  font-family: 'Lilita One', cursive;
  font-size: 20px;
}
</style>
