<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <movie-search></movie-search>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import MovieSearch from '@/components/MovieSearch.vue'

export default {
  name: 'home',
  components: {
    HelloWorld,
    MovieSearch
  }
}
</script>
