<template>
    <div class="movie">
        <div v-if='error'>{{error}}</div>
        <div v-else>
            {{movie.Title}}
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import config from '@/config';

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
  created(){
      let url = config.baseApiUrl + config.apiKey + '&i=' + this.movieId;
      axios.get(url)
      .then(response => this.movie = response.data)
      .catch(error => this.error = error)
  }
};
</script>

<style lang="scss" scoped>
.movie {
  //text-align: center;
}
</style>
