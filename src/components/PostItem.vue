<template>
	<div class="post">
		<li v-if="item.data.stickied === false">
			<div class="post">
				<a :href="item.data.url" :style="getImageBackgroundCSS(item.data.thumbnail)" target="_blank" class="thumbnail"></a>
				<div class="details">
					<a :href="item.data.url" :title="item.data.title" target="_blank" class="title">
						{{ item.data.title | truncate}}
					</a>			
					<div class="action-buttons">
						<a :href="'http://reddit.com' + item.data.permalink " title="Vote">
							<i class="material-icons">thumbs_up_down</i>
							{{item.data.score}}
						</a>
						<a :href="'http://reddit.com' + item.data.permalink " title="Go to discussion">
							<i class="material-icons">forum</i>
							{{item.data.num_comments}}
						</a>
						<a class="favs"
					 		v-on:click="addToFavs(item.data)" 
					 		:input="item.data"
					 		v-if="!isFav"
					 		@click="toggle">
					 		<span>Add To Favourites</span>
					 	</a>
					</div>
				</div>
			</div>
		</li>
	</div>
</template>

<script>

export default {
	name: 'PostItem',
 	props: {
    	item: {},
    	added: Boolean
  	},
  	data: function () {
      return {
      	favouritesArray: [],
      	isFav: false
      }
    },
    computed: {
    	
    },
  	methods: {
  		getImageBackgroundCSS: function (image) {
  			let ImageBackground = image

  			return {
  				"background-image": 'url('+ImageBackground+')'
  			}
  		},
  		addToFavs: function(input) {
  			this.$emit('add-favs', input)
  		},
  		toggle: function() {
    		this.isFav = !this.isFav
    	}
    }
}
</script>

<style type="text/css">
	.favs:hover {
		cursor: pointer;
	}
</style>