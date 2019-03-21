<template>
  <div id="app">
    <Favourite 
      v-if="favouritesArray.length > 0"
      name="Favourites"
      :favs="favouritesArray"
      @favs-removed="removeFromFavs"> 
    </Favourite>
    <Subreddit name="cats" 
      @favs-update="addToFavs">
    </Subreddit>
    <Subreddit name="kittens" 
      @favs-update="addToFavs">
    </Subreddit>
  </div>
  
</template>

<script>
import Subreddit from './components/Subreddit.vue'
import Favourite from './components/Favourites.vue'

export default {
  name: 'app',
  components: {
    Subreddit,
    Favourite
  },
  props: {
    input: {},
    favs: []
  },
  data: function () {
      return {
          favouritesArray: []
      }
  },
  methods: {
    addToFavs: function(e) {
        this.favouritesArray.push(e);
        console.log(e)
      },
      removeFromFavs: function(e) {
        this.favouritesArray.splice(e, 1);
      }
  }
}
</script>

<style>
  @import './assets/css/styles.css';
</style>
