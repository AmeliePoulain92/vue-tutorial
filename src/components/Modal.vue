<template>
	<div class="modal">
		<div class="modal-inner">
			<input type="text" ref="title" v-model="updatedData.title" />

			<!-- <ul>
				<li v-for="error in errors.title">
					<slot :error="error">{{error}}</slot>
				</li>
			</ul> -->

			<footer class="modal-footer">
				<button type="button" @click="close">Cancel</button>
				<button type="button" :disabled="button_states.save.disabled">Save</button>
			</footer>
		</div>
	</div>
</template>

<script>
export default {
	name: 'modal',
	props: ['settings'],
	data () {
		return {
			updatedData: {},
			button_states: {
				save: {
					disabled: true
				}
			},
			errors: {
				title: ['error1']
			}
		}
	},
	methods: {
		close () {
			this.settings.show = false
		}
	},

	watch: {
		updatedData: {
			handler (n, o) {
				if (!_.isEmpty(o)) {
					this.button_states.save.disabled = false
				}
			},
			deep: true
		}
	},

	mounted () {
		this.updatedData = _.cloneDeep(this.settings.data)

		this.$refs.title.focus()
	}
}
</script>

<style lang="scss" scoped>
.modal {
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	z-index: 9999;
	background-color: rgba(#000, 0.3);
	&-inner {
		position: absolute;
		top: 50%;
		left: 50%;
		padding: 20px;
		transform: translate(-50%, -50%);
		background-color: #fff;
	}
}
</style>