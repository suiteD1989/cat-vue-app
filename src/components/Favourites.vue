<template>
	<div class="subreddit">
		<h2>{{ name | uppercase }}</h2>
		<ul class="item-list">
      <FavouritePosts v-for="fav in favs"
        :item="fav" 
        :key="fav.id" 
        @add-favs="addToFavs"
        @remove-favs="removeFromFavs">
      </FavouritePosts>
    </ul>
	</div>
</template>

<script>

import axios from 'axios'
import FavouritePosts from './FavouritePost.vue'

export default {
	name: 'Favourite',
	props: {
		name: String,
    favs: {}
	},
	components: {
    FavouritePosts,
	},
  data: function () {
    return {
        favouritesArray: []
    }
  },
  methods: {
    addToFavs: function(input) {
        this.favouritesArray.push(e);
      },
      removeFromFavs: function(input) {
        this.$emit('favs-removed', input.data)
      }
  },
  mounted: function () {
    console.log('fav mounted')
    console.log(favouritesArray)
  }
}
</script>