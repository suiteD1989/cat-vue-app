<template>
	<div class="subreddit">
		<h2>{{ name | uppercase }}</h2>
		<ul class="item-list">
			<PostItem 
				v-if="name === 'cats'" 
				v-for="post in catPosts " 
				:item="post" 
				:input="post"
				@add-favs="addToFavs(post)">		
			</PostItem>
			<PostItem 
				v-if="name === 'kittens'" 
				v-for="post in kittenPosts " 
				:item="post"
				:input="post"
				@add-favs="addToFavs(post)">
			</PostItem>
		</ul>
	</div>
</template>

<script>

import axios from 'axios'
import PostItem from './PostItem.vue'

export default {
	name: 'Subreddit',
	props: {
		name: String,
		item: {},
		input: {}
	},
	components: {
		PostItem,
	},
	data: function () {
  		return {
        	kittenPosts: Array,
        	catPosts: Array
  		}
    },
    methods: {
  		fetchCatPosts: function() {
    		axios.get('https://www.reddit.com/r/cats.json?limit=5').then((response) => {
      			return	this.catPosts = response.data.data.children
        	}, (error) => {
          		console.log(error)
        	})
    	},
    	fetchKittenPosts: function() {
    		axios.get('https://www.reddit.com/r/kittens.json?limit=5').then((response) => {
      			return this.kittenPosts = response.data.data.children
        	}, (error) => {
          		console.log(error)
        	})
    	},
  		fetchRedditPosts: function () {
        	axios.all([this.fetchCatPosts(), this.fetchKittenPosts()])
		  		.then(axios.spread(function (acct, perms) { 
		  	}));
      	},
      	addToFavs: function(input) {
  			this.$emit('favs-update', input.data)
  		}
    },
    mounted: function () {
      this.fetchRedditPosts()
    }
}
</script>