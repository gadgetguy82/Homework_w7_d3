<template lang="html">
  <li v-on:click="handleClick">{{country}}</li>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "list-item",
  props: ["country"],
  methods: {
    handleClick() {
      eventBus.$emit("country-selected", this.country);
      this.$parent.$parent.handleFocusOut();
    },
    // handleFocusIn() {
    //   eventBus.$emit("itemClicked", [on:focus])
    // }
  }
}
</script>

<style lang="css" scoped>
li {
  left: 0;
  right: 0;
  border: 1px solid #DCDCDC;
  cursor: pointer;
  padding: 10px;
  z-index: 99;
  background-color: #D3D3D3;
  width: 100%;
  white-space: nowrap;
}

li:hover {
  background-color: #E9E9E9;
}

li:active {
  background-color: #1E90FF;
  color: #FFFFFF;
}
</style>
