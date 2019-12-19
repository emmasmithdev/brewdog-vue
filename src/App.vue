<template>
  <div id="app">
    <h1>Brewdog Beers</h1>
    <div class="main-container">
      <beers-list :beers="beers"></beers-list>
      <beer-details v-if="selectedBeer" :beer="selectedBeer"></beer-details>
      <favourite-beers :favouriteBeers="favouriteBeers"></favourite-beers>
    </div>
  </div>
</template>

<script>
  import BeersList from './components/BeersList.vue'
  import {eventBus} from './main.js'
  import BeerDetails from './components/BeerDetails.vue'
  import FavouriteBeers from './components/FavouriteBeers.vue'

  export default {
    name: 'app',
    data(){
      return {
        beers: [],
        selectedBeer: null,
        favouriteBeers: []
      };
    },
    mounted(){
      fetch('https://api.punkapi.com/v2/beers')
      .then(res => res.json())
      .then(beers => this.beers = beers)

      eventBus.$on("beer-selected", (beer) => {
        this.selectedBeer = beer
       })

      eventBus.$on("beer-favourited", (beer) => {
        if (!this.favouriteBeers.includes(beer)){
          this.favouriteBeers.push(beer)
        }
      })
      eventBus.$on("beer-removed", (beer) => {
        const index = this.favouriteBeers.indexOf(beer)
        if (index > -1){
          this.favouriteBeers.splice(index, 1);
        }
      })
     },
   components: {
     'beers-list': BeersList,
     'beer-details': BeerDetails,
     'favourite-beers': FavouriteBeers
   }
 }
</script>

<style lang="css" scoped>

</style>
