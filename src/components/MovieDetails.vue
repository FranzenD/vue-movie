<template>  
<div class="details"> 
  <div v-if='error' class="error">{{error}}</div>
  <div v-if="showError">
    {{movie.Error}}
  </div>
  <div v-else>
    <div class="movie">
    <section class="movie__title">
      {{movie.Title}}            
    </section>       
    <section class="movie__poster">
      <img :src="movie.Poster" class="img-responsive"/>
    </section>   
    <section class="movie__details">
      {{movie.Plot}}    
    </section> 
  </div>
  </div>
  </div> 
</template>

<script>
import axios from "axios";
import config from "@/config";

export default {
  name: "MovieDetails",
  data() {
    return {
      movieId: this.propMovieId,
      movie: {},
      error: null
    };
  },
  props: {
    propMovieId: String
  },
  computed:{
    showError() {
      return this.movie.Response && this.movie.Response ==='False';
    }
  },
  created() {
    let url = config.baseApiUrl + config.apiKey + "&i=" + this.movieId;
    axios
      .get(url)
      .then(response => (this.movie = response.data))
      .catch(error => (this.error = error));
  }
};
</script>

<style lang="scss" scoped>

.movie {
  margin-top: 50px;
  display: grid;
  grid-gap: 10px;
  grid-template-columns: 25% auto;
  grid-template-rows: 60px auto;
  grid-template-areas:
    "header header"
    "right main";

  &__title {
    grid-area: header;
    font-size: 32px;
  }

  &__details {
    grid-area: main;
    justify-self: start;
    text-align: left;
  }

  &__poster {
    grid-area: right;
  }
}

.card {
  padding: 20px;
  border: solid 1px $borderColor;
}
</style>
