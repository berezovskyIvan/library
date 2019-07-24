<template lang="pug">
    label.position(@click="changeChecked")
        .boxBorder(:style="bloom") &#10003
</template>

<script>
	export default {
		name: 'customCheckBox',
		props: {
			checked: {
				type: Boolean,
				default: false
			},
			disabled: {
				type: Boolean,
				default: false
			},
			color: {
				type: String,
				default: '#9575cd'
			}
		},
		computed: {
			bloom: function() {
                 if (this.checked) {
					return { backgroundColor: this.color, border: '1.3px solid ' + this.color, cursor: 'pointer' }
				} else {
					return { backgroundColor: '#fff', border: '1.3px solid #8eacbb', cursor: 'pointer' }
				}
			}
		}
	}
</script>

<style  scoped>

</style>
