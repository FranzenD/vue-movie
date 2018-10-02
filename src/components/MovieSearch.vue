<template>
<div class="movie-search">
    <input type="search" v-model="searchString" @keyup.enter="searchMovie">
    <button type="button" @click="searchMovie">Sök</button>

    <div v-if="searchResult && searchResult.Search">
        <ul>
            <li v-for="(result, index) in searchResult.Search" :key="index">{{result.Title}}</li>
        </ul>
    </div>
</div>

</template>

<script>
import axios from "axios";

const baseApiUrl = "http://www.omdbapi.com/?apikey=bca47ba&";

export default {
  name: "MovieSearch",
  data() {
    return {
      searchString: "",
      searchResult: {}
    };
  },
  props: {},
  methods: {
    searchMovie() {
      let url = baseApiUrl + "s=" + this.searchString;
      let result = axios
        .get(url)
        .then(response => (this.searchResult = response.data))
        .catch(error => console.log(error));
    }
  }
};
</script>

<style lang="scss" scoped>
.movie-search {
  & input {
    padding: 10px;
    font-size: 20px;
  }
}
</style>
