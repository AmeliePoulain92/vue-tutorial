<template>
	<li>
		<button type="button" @click="edit" v-if="data.title">Edit</button>

    <h3>{{ data.title }}</h3>
    <h4>{{ data.year }}</h4>

    <img :src="data.poster" :alt="data.title" />
  </li>
</template>

<script>
export default {
	name: 'movie',
	props: ['data'],

	methods: {
		edit () {
			this.$emit('edit', this.data.id)
		}
	}
}
</script>