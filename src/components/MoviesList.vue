<template>
  <div>
    <h1>Movies list</h1>

    <ul class="movies" v-if="moviesList && moviesList.length">
      <movie
        v-for="(movie) in moviesList"
        :key="movie.id"
        @edit="onMovieEdit"
        :data="movie" />
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
import Movie from './Movie.vue'

export default {
  components: {
    Movie
  },

  data () {
    return {
      moviesList: []
    }
  },

  mounted () {
    axios.get('https://api.myjson.com/bins/t9mzc')
    .then(moviesResponse => this.moviesList = moviesResponse.data)
  },

  methods: {
    onMovieEdit (object) {
      console.log('onMovieEdit', object)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
