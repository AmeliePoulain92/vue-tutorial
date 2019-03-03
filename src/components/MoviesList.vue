<template>
  <div>
    <h1>Movies list</h1>

    <input type="search" v-model="filters.searchQuery" placeholder="Search for movie" />

    <ul class="genres">
      <li v-for="genre in genres">
        <label>
          {{genre}}
          <input type="checkbox" v-model="filters.genres" :value="genre" />
        </label>
      </li>
    </ul>

    <ul class="movies" v-if="data && data.length">
      <movie
        v-for="(movie) in data"
        :key="movie.id"
        @edit="onMovieEdit"
        :data="movie" />
    </ul>
  </div>
</template>

<script>
import Movie from './Movie.vue'

export default {
  props: ['data', 'genres', 'filters'],
  components: {
    Movie
  },

  data () {
    return {

    }
  },

  methods: {
    onMovieEdit (id) {
      let editedMovie = this.data.find(m => m.id === id)
      this.$emit('edit', editedMovie)
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.genres {
  list-style: none;
  margin-bottom: 45px;
}

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
