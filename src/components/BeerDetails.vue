<template lang="html">
  <div>
    <h3>{{beer.name}}</h3>
    <p>{{beer.tagline}}</p>
    <button v-on:click="addToFavourites">Add to Favourites</button>
    <button v-on:click="removeFromFavourites">Remove from Favourites</button>
    <p>First Brewed: {{beer.first_brewed}}</p>
    <p>Description: {{beer.description}}</p>
    <h4>Food Pairings:</h4>
    <p v-for="(food, index) in beer.food_pairing" :food="food"
    :key="index" :value="food">{{food}}</p>
    <h4>Ingredients:</h4>
    <h5>Malt:</h5>
    <p v-for="(ingredient, index) in beer.ingredients.malt" :malt="malt"
    :key="index" :value="malt">{{ingredient.name}}</p>
    <h5>Hops:</h5>
    <p v-for="(ingredient, index) in beer.ingredients.hops" :hops="hops"
    :key="index" :value="hops">{{ingredient.name}}</p>
    <h5>Yeast:</h5>
    <p>{{beer.ingredients.yeast}}</p>
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
    },
    removeFromFavourites: function(){
      this.favouriteBeer = this.beer;
      eventBus.$emit("beer-removed", this.favouriteBeer)
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
