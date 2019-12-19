<template lang="html">
  <div>
    <h4>Favourite Beers</h4>
    <li v-for="(beer, index) in this.favouriteBeers" :beer="beer"
    :key="index" :value="beer">{{beer.name}}</li>
  </div>
</template>

<script>
export default {
  name: "favourite-beers",
  props: ['favouriteBeers'],
}
</script>

<style lang="css" scoped>
</style>
