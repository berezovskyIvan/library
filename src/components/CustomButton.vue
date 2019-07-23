<template lang="pug">
	custom-tooltip(value="Добавить")
		slot
			.button-block(:style="bloom")
				.plus-icon &#43
</template>

<script>
	import customTooltip from './CustomTooltip'

	export default {
		name: 'customButton',
		components: {
			customTooltip
		},
		props: {
			diameter: {
				type: String,
				default: '50px'
			},
			color: {
				type: String,
				default: '#4dd0e1'
			}
		},
		computed: {
			bloom: function() {
				return {
					height: this.diameter,
					width: this.diameter,
					background: this.color
				}
			}
		}
	}
</script>

<style scoped>
	.button-block {
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		color: #fff;
	}
	
	.button-block:hover {
		cursor: pointer;
		opacity: 0.7;
	}
	
	.plus-icon {
		font-size: 60px;
		font-weight: bold;
		user-select: none;
	}
</style>
