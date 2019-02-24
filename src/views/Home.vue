<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <movies-list @edit="onMovieEdit" :data="moviesList" />

    <modal
      v-if="movieModalSettings.show"
      :settings="movieModalSettings"
      @saveMovie="onMovieSave">
        <template slot="errors" slot-scope="{error}">
          <div class="errors highlighted">{{error.message}}</div>
        </template>
    </modal>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import MoviesList from '@/components/MoviesList.vue'
import Modal from '@/components/Modal.vue'

export default {
  name: 'home',
  components: {
    MoviesList,
    Modal
  },

  data () {
  	return {
  		moviesList: [],
      movieModalSettings: {
        show: false
      }
  	}
  },

  methods: {
  	onMovieEdit (movie) {
      this.movieModalSettings.data = movie
      this.movieModalSettings.show = true
    },

    onMovieSave (movie) {
      let updatedMovieIndex = _.findIndex(this.moviesList, m => m.id === movie.id)

      if (updatedMovieIndex !== -1) {
        this.$set(this.moviesList, updatedMovieIndex, movie)
      }
    }
  },

  mounted () {
    axios.get('https://api.myjson.com/bins/t9mzc')
    .then(moviesResponse => this.moviesList = moviesResponse.data)
  },
}
</script>

<style lang="scss" scoped>
  .errors {
    color: red;
  }
</style>
