<template lang="html">
  <li class="list-element" v-if="this.status || (!this.status && !favoriteFilter)">
      <h3>{{beer.name}}</h3>

      <div class="article-buttons">

        <img v-if="!status" src="/unchecked.svg" v-on:click="status = !status">
        <img v-if="status" src="/checked.svg" v-on:click="status = !status">
        <img v-on:click="grabABeer" src="/info.svg">
      </div>
      <!-- <input type="checkbox" id="favorite" v-model="status">
      <label for="favorite" v-if="!status">Add to favorites</label> -->

    <div class="article-bottom">

      <div class="article-right">
        <p>ABV: {{beer.abv}}%</p>
        <p>"{{beer.tagline}}"</p>
      </div>

      <img class="beer-icon" src="../../public/beer_icon.svg"/>

    </div>

  </li>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'beer-component',
  props: ['beer', 'favoriteFilter'],
  data() {
    return {
      status: false
    }
  },
  methods: {
    grabABeer() {
      eventBus.$emit('beer-in-hand', this.beer);
    }
  }
}
</script>

<style lang="css" scoped>

li {
  display: flex;
  flex-direction: column;
  margin: 0.2em;
  max-width: 40%;
  border: 3px solid #669999;
  justify-content: flex-start;
  border-radius: 2%;
  flex-grow: 1;
}

.article-top {
  /* border: 1px dotted #ccc; */
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.article-buttons {
  display:flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: flex-end;
  max-height: 3em;
  margin: 1em;
}

.article-buttons img{
  max-height: 3em;
  margin: 0 1em;
}

.article-top {
  max-width: 1em;
  margin: 1em;

}

.article-bottom {
  /* border: 1px dotted #ccc; */
  display: flex;
  flex-direction: row-reverse;
}

.article-right {
  /* border: 1px dotted #ccc; */
  display: flex;
  flex-direction: column;
  max-width: 40%;
  flex-wrap: wrap;
}

.beer-icon {
  width: 3em;
  padding: 1em;
}

h3 {
  font-family: 'Open Sans', sans-serif;
  font-weight: 800;
  font-size: 2em;
  display: flex;
  flex-wrap: wrap;
  color: #fff;
  padding: 0.5em;
  background-color: #339999;
  /* border: 0.2em solid #669999; */
  margin-top: 0;
}
</style>
