<template lang="html">
  <div>
    <label for="beer_select">Select a Beer:</label><br>
        <select id="beer_select" v-on:change="handleChange" v-model="selectedBeer">
          <option disabled value="">Select a beer</option>
          <option v-for="(beer, index) in beers" :key="index" :value="beer">{{beer.name}}</option>
        </select>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
    name: 'beers-list',
    data(){
      return{
        selectedBeer: null
      }
    },
    props: ['beers'],
    methods: {
      handleChange(event){
        eventBus.$emit('beer-selected', this.selectedBeer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
