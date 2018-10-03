<template>
<div class="movie-search">
    <input type="search" v-model="searchString" @keyup.enter="searchMovie">
    <button type="button" @click="searchMovie">Sök</button>

<div v-if='error'>{{error}}</div>
    <div v-if="searchResult && searchResult.Search" class="search-result">
        <div v-for="(result, index) in searchResult.Search" :key="index" class="movie">
            <div class='movie__poster'>
                <img :src='result.Poster' />
            </div>
            <div class='movie__title'>
                {{result.Title}}
            </div>
        </div>                    
    </div>
</div>

</template>

<script>
import axios from "axios";
import config from "@/config";

const baseApiUrl = "http://www.omdbapi.com/?apikey=";

export default {
  name: "MovieSearch",
  data() {
    return {
      searchString: "",
      searchResult: {},
      error: ""
    };
  },
  props: {},
  methods: {
    searchMovie() {
      let url = baseApiUrl + config.apiKey + "&s=" + this.searchString;
      axios
        .get(url)
        .then(response => (this.searchResult = response.data))
        .catch(error => {
          this.error = error;
        });
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
.search-result{
    display: grid;
    grid-template-columns: 50% 50%;
    grid-gap: 20px;
}
.movie {
  text-align: left;
  display: grid;
  grid-template-columns: 100px auto;
  grid-gap: 10px;
  padding: 10px;

  &__poster {
    img {
      max-width: 100%;
      height: auto;
    }
  }
  &__title {
    font-size: 2rem;
    font-family: Arial, Helvetica, sans-serif;
  }
}
</style>
