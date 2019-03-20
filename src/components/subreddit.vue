<template>
	<div class="subreddit">
		<h2>{{ name }}</h2>
		<ul class="item-list">
			<postItem v-for="post in posts " :item="post"></postItem>
		</ul>
	</div>
</template>

<script>

import axios from 'axios'
import PostItem from './PostItem.vue'

export default {
	name: 'subreddit',
	props: {
		post: Array,
		name: String,
	},
	components: {
		PostItem
	},
	data: function () {
  		return {
        	posts: Array
  		}
    },
    methods: {
  		fetchCatPosts: function() {
    		axios.get('https://www.reddit.com/r/cats.json?limit=5').then((response) => {
      			return	this.posts = response.data.data.children
        	}, (error) => {
          		console.log(error)
        	})
    	},
    	fetchKittenPosts: function() {
    		axios.get('https://www.reddit.com/r/kittens.json?limit=5').then((response) => {
      			return this.posts = response.data.data.children
        	}, (error) => {
          		console.log(error)
        	})
    	},
  		fetchRedditPosts: function () {
        	axios.all([this.fetchCatPosts(), this.fetchKittenPosts()])
		  		.then(axios.spread(function (acct, perms) {
				console.log(name)   
		  	}));
      	}
    },
    mounted: function () {
      this.fetchRedditPosts()
    }
}
</script>