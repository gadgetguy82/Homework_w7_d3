<template lang="html">
  <option>{{country.name}}</option>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "list-item",
  props: ["country"]
}
</script>

<style lang="css" scoped>
</style>
