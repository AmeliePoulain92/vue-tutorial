<template>
	<li>
		<button type="button" @click="editTitle()" v-if="data.title">Edit</button>

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
		editTitle () {
			this.$emit('edit-title', {title: 'test', index: 0})
		}
	}
}
</script>