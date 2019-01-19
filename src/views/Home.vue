<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <MoviesList />
  </div>
</template>

<script>
// @ is an alias to /src
import MoviesList from '@/components/MoviesList.vue'

export default {
  name: 'home',
  components: {
    MoviesList
  },

  data () {
  	return {
  		data: {
  			id: undefined,
  			title: '',
  			content: ''
  		}
  	}
  },

  methods: {
  	onChangeContent (value) {
  		var confirmTest = confirm('Confirm?')

  		if (confirmTest) {
  			this.data.content = 'parent ' + value
  		} else {
  			alert('NO!!!!!')
  		}
  	},

  	alertMethod () {
  		alert('alertMethod')
  	}
  }
}
</script>
