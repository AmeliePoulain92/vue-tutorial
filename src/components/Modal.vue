<template>
	<div class="modal" ref="modal">
		<div class="modal-inner">
			<div class="modal-item">
				<input
					type="text"
					ref="title"
					name="title"
					:required="fieldSettings.title.required"
					v-model="updatedData.title"
					class="modal-field" />

					<div class="errors" v-if="errors && errors.title && errors.title.length">
						<slot name="errors" :error="error" v-for="error in errors.title">{{error.message}}</slot>
					</div>
			</div>

			<div class="modal-item">
				<textarea
					v-model="updatedData.content"
					name="content"
					cols="30"
					rows="10"
					:required="fieldSettings.content.required"
					class="modal-field"></textarea>

					<div class="errors" v-if="errors && errors.content && errors.content.length">
						<slot name="errors" :error="error" v-for="error in errors.content">{{error.message}}</slot>
					</div>
			</div>

			<footer class="modal-footer">
				<button type="button" @click="close">Cancel</button>
				<button type="button" :disabled="button_states.save.disabled" @click="save">Save</button>
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
			messages: {
				fields: {
					required: 'This field is required'
				}
			},
			fieldSettings: {
				title: {
					required: true
				},
				content: {
					required: false
				}
			},
			errors: {}
		}
	},

	computed: {
		requiredFields () {
			return Object.entries(this.fieldSettings)
					.filter(item => item[1].required)
					.map(item => item[0])
		},

		hasErrors () {
			return !!_.flatten(Object.values(this.errors)).length
		}
	},

	methods: {
		errorsHandler (data) {
			for (let prop in data) {
				// required check
				if (!data[prop] && this.requiredFields.includes(prop)) {
					console.log('test')
					this.clearErrorsByFieldName(prop)

					this.errors[prop].push({
						type: 'required',
						message: this.messages.fields.required
					})
				} else {
					this.clearErrorsByFieldName(prop)
				}
			}
		},

		clearErrorsByFieldName (field) {
			this.$set(this.errors, field, [])
		},

		close () {
			this.settings.show = false
		},

		save () {
			this.$emit('saveMovie', this.updatedData)
			this.close()
		}
	},

	watch: {
		updatedData: {
			handler (n) {
				if (n) {
					this.errorsHandler(n)
					this.button_states.save.disabled = _.isEqual(n, this.settings.data) || this.hasErrors
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

.errors {
	list-style: none;
	padding-left: 0;
	&.highlighted {
		color: red;
	}
}
</style>