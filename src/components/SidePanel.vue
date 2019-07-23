<template lang="pug">
	.side-panel
		div &#10006
</template>

<script>
	export default {
		name: 'sidePanel'
	}
</script>

<style scoped>
	.side-panel {
		position: absolute;
		height: 100%;
		width: 300px;
		top: 0;
		right: 0;
		border-left: 1px solid #4dd0e1;
		background: #fff;
	}
</style>
