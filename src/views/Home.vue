<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <movies-list @edit="onMovieEdit" />

    <modal
      v-if="movieModalSettings.show"
      :settings="movieModalSettings" />
  </div>
</template>

<script>
// @ is an alias to /src
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
  		data: {
  			id: undefined,
  			title: '',
  			content: '',
  		},
      movieModalSettings: {
        show: false
      }
  	}
  },

  methods: {
  	onMovieEdit (movie) {
      this.movieModalSettings.data = movie
      this.movieModalSettings.show = true
    }
  }
}
</script>
