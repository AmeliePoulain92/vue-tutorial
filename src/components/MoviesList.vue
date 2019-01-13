<template>
  <div>
    <h1>Movies list</h1>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'MoviesList',
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
      internalData: {
        id: undefined,
        title: '',
        content: ''
      }
    }
  },

  mounted () {
    axios.get('https://api.myjson.com/bins/e2ilc')
  },

  methods: {
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
