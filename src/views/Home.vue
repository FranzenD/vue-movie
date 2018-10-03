<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <movie-search></movie-search>
  </div>
</template>

<script>
// @ is an alias to /src
import MovieSearch from "@/components/MovieSearch.vue";

export default {
  name: "home",
  components: {
    MovieSearch
  }
};
</script>
