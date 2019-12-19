<template lang="html">
  <div>
    <h3>{{beer.name}}</h3>
    <p>{{beer.tagline}}</p>
    <button v-on:click="addToFavourites">Add to Favourites</button>
    <p>First Brewed: {{beer.first_brewed}}</p>
    <p>Description: {{beer.description}}</p>
    <h4>Food Pairings:</h4>
    <p v-for="(food, index) in beer.food_pairing" :food="food"
    :key="index" :value="food">{{food}}</p>
    <img :src="beer.image_url" />
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'beer-details',
  data(){
    return{
      favouriteBeer: null
    }
  },
  props: ['beer'],
  methods: {
    addToFavourites: function(){
      this.favouriteBeer = this.beer;
      eventBus.$emit("beer-favourited", this.favouriteBeer)
      this.favouriteBeer = null;
    }
  }
}
</script>

<style lang="css" scoped>
  img {
    max-width: 100px;
    height: auto;
  }
</style>
