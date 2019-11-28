<template lang="html">

<div>
  <header>
    <section id="header-left">
    <img src='/abv-logo.svg'>
    <button id="favourite-switch" type="button" v-on:click="favoriteFilter = !favoriteFilter"><h1>{{ favoriteFilter ? "Show All" : "Show Favorites" }}</h1></button>
  </section>
      <beer-label :beer='selectedBeer'></beer-label>
  </header>
  <main>
    <beers-list :beers='beers' :favoriteFilter='favoriteFilter'></beers-list>
  </main>

</div>


</template>

<script>

import BeersList from './components/BeersList.vue';
import BeerLabel from './components/BeerLabel.vue';
import {eventBus} from './main.js';

export default {
  name:'app',
  data() {
    return {
      beers: [],
      selectedBeer: null,
      favoriteFilter: false
    }
  },
  mounted(){
    fetch('https://api.punkapi.com/v2/beers')
    .then(response => response.json())
    .then(beers => this.beers = beers)

  eventBus.$on('beer-in-hand', (beer) => {
    this.selectedBeer = beer
  })
  },
  components: {
    "beers-list": BeersList,
    "beer-label": BeerLabel
  }
}
</script>

<style lang="css" scoped>
body {
  font-family: 'Open Sans', sans-serif;

}

header {
  display: grid;
  grid-template-columns: 2fr 5fr;
}
header img {
  max-width: 80%;
}
#header-left {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

#beer-label {

}

#favourite-switch{
  background-color: #339999;
  margin: 2em;
}
</style>
