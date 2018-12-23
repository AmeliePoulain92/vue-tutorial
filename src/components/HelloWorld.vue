<template>
  <div class="hello">
    <h1>
      <template v-if="mode === 'edit'">
        Edit Your data
      </template>
      <template v-else>
        Create data from scratch
      </template>
    </h1>

    <input type="text" :value="data.title" />
    <textarea cols="30" rows="10" :value="data.content" @change="changeContent"></textarea>

    <button @click="updateData" v-if="mode === 'edit'">Edit</button>
    <button @click="createData" v-else>Create</button>

    <slot>default</slot>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
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
