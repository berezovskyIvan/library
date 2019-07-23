<template lang="pug">
	.tooltip
		slot
		.tooltip-text {{ value }}
</template>

<script>
	export default {
		name: 'customTooltip',
		props: {
			value: {
				type: String,
				default: ''
			}
		}
	}
</script>

<style scoped>
	.tooltip .tooltip-text {
	  visibility: hidden;
	  width: 120px;
	  background-color: #555;
	  color: #fff;
	  text-align: center;
	  padding: 5px 0;
	  border-radius: 6px;

	  position: absolute;
	  z-index: 1;
	  bottom: 110%;
	  left: 50%;
	  margin-left: -75px;

	  opacity: 0;
	  transition: opacity 0.3s;
	}

	.tooltip .tooltip-text::after {
	  content: "";
	  position: absolute;
	  top: 100%;
	  left: 50%;
	  margin-left: -5px;
	  border-width: 5px;
	  border-style: solid;
	  border-color: #555 transparent transparent transparent;
	}

	.tooltip:hover .tooltip-text {
	  visibility: visible;
	  opacity: 1;
	}
</style>
