<template>
<div class="moogle">
  <div class="search-field">
  <div class="movie-search">
    <input type="search" class="movie-search__input" v-model="searchString" @keyup.enter="searchMovie" />
    <button type="button" class="movie-search__button" @click="searchMovie">Sök</button>
  </div>
  </div>

    <div v-if="error" class="error">{{error}}</div>
    <div v-if="searchResult.Response && !JSON.parse(searchResult.Response.toLowerCase())" class="error">
      {{searchResult.Error}}
    </div>
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
  },
  computed: {}
};
</script>

<style lang="scss" scoped>
$shadowColor: #a4a8ac;
.search-field{
  display:flex;
  justify-content: center;
}

.movie-search {
  display: inline-flex;
  flex: 0 0 70%;
  border: solid 1px #d3cdcd;
  justify-content: center;
  flex-direction: row;

  &__input {
    -webkit-appearance: none;
    flex-grow: 2;
    padding: 10px;
    font-size: 22px;
    border: none;

    &:focus {
      outline: none;
    }
  }

  &__button {
    -webkit-appearance: none;
    border: none;
    background: blue;
    border: solid 1px blue;
    color: white;
    width: 60px;

    &:focus {
      outline: none;
    }
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
  border: solid 1px $shadowColor;
  box-shadow: $shadowColor 5px 5px 5px 2px;

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