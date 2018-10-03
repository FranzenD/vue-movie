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
                <router-link :to="{name: 'moviedetails', params: {id: result.imdbID}}">{{result.Title}}</router-link>
            </div>
        </div>                    
    </div>
</div>

</template>

<script>
import axios from "axios";
import config from "@/config";

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
      let url = config.baseApiUrl + config.apiKey + "&s=" + this.searchString;
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
$shadow-color: #a4a8ac;

.movie-search {
  & input {
    padding: 10px;
    font-size: 20px;
  }
}
.search-result {
  margin-top: 30px;
  display: grid;
  grid-template-columns: 50% 50%;
  grid-gap: 20px;
  padding: 20px 40px 20px 20px;

  @media screen and (min-width: 1024px) {
    grid-template-columns: 33% 33% 33%;
  }
  @media screen and (max-width: 768px) {
    grid-template-columns: 100%;
  }
}
.movie {
  text-align: left;
  display: grid;
  grid-template-columns: 100px auto;
  grid-gap: 10px;
  padding: 10px;
  border: solid 1px $shadow-color;
  box-shadow: $shadow-color 5px 5px 5px 2px;

  &__poster {
    img {
      max-width: 100%;
      height: auto;
    }
  }
  &__title {
    font-size: 1.7rem;
    font-family: Arial, Helvetica, sans-serif;
    text-align: center;

    @media screen and (min-width: 1024px) {
      font-size: 1.5rem;
    }
    @media screen and (max-width: 768px) {
      font-size: 2rem;
    }
  }
}
</style>
