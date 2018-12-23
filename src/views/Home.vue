<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>title: {{data.title}}</h1>
    <p>content: {{data.content}}</p>

    <HelloWorld msg="Edit Modal" mode="edit" :data="data" v-if="data.id" />
    <HelloWorld msg="Create modal" mode="create" v-else :data="data" :func="() => this.alertMethod()" @update:content="onChangeContent">
    	not default
    </HelloWorld>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
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
