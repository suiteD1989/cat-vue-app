<template>
  <div id="app">
    <subreddit name="cats"></subreddit>
    <subreddit name="kittens"></subreddit>
  </div>
  
</template>

<script>
import subreddit from './components/subreddit.vue'

export default {
  name: 'app',
  components: {
    subreddit
  }
}
</script>

<style>
  @import './assets/css/styles.css';
</style>
