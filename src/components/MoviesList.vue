<template>
  <div>
    <h1>Movies list</h1>

    <ul class="movies" v-if="moviesList && moviesList.length">
      <movie
        v-for="(movie, index) in moviesList"
        :key="index"
        @edit-title="onUpdateTitle"
        :data="movie" />
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
import Movie from './Movie.vue'

export default {
  name: 'MoviesList',
  components: {
    Movie
  },
  props: {
    msg: String,
    mode: String,
    data: {
      type: Object
    },
    func: Function
  },

  data () {
    return {
      moviesList: []
    }
  },

  beforeMount () {
    console.log('hook beforeMounted')
  },

  mounted () {
    console.log('hook mounted')

    axios.get('https://api.myjson.com/bins/t9mzc')
    .then(moviesResponse => this.moviesList = moviesResponse.data)
  },

  methods: {
    onUpdateTitle (object) {
      this.moviesList[object.index].title = object.title
    },

    changeContent ($event) {
      this.$emit('update:content', $event.target.value)
    },

    createData () {
      this.func()

      // this.data.id = Math.random(1, 5)
      // this.data.content = this.internalData.content
    },

    updateData () {
      alert('updateData')
    }
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
