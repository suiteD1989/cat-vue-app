<template>
	<div class="post">
		<li>
			<div class="post">
				<a :href="item.url" :style="getImageBackgroundCSS(item.thumbnail)" target="_blank" class="thumbnail"></a>
				<div class="details">
					<a :href="item.url" :title="item.title" target="_blank" class="title">
						{{ item.title | truncate}}
					</a>			
					<div class="action-buttons">
						<a :href="'http://reddit.com' + item.permalink " title="Vote">
							<i class="material-icons">thumbs_up_down</i>
							{{item.score}}
						</a>
						<a :href="'http://reddit.com' + item.permalink " title="Go to discussion">
							<i class="material-icons">forum</i>
							{{item.num_comments}}
						</a>
						<a v-on:click="removeFromFavs(item)">
							<i class="material-icons remove-fav">delete</i>
						</a>
					</div>
				</div>
			</div>
		</li>
	</div>
</template>


<script>

export default {
	name: 'FavouriteItems',
 	props: {
    	item: {}
  	},
  	methods: {
  		getImageBackgroundCSS: function (image) {
  			let ImageBackground = image

  			return {
  				"background-image": 'url('+ImageBackground+')'
  			}
  		},
  		removeFromFavs: function(input) {
  			this.$emit('remove-favs', input)
  		}
    },
}
</script>

<style type="text/css">
	.remove-fav:hover {
		cursor: pointer;
	}
</style>