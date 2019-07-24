<template lang="pug">
	div
		.info-row
			.settings.p-right &#9776
			.info-text Открыть меню настроек
		.info-row
			custom-button.p-right(diameter="30px", iconSize="35px")
			.info-text Добавить книгу
</template>

<script>
	import customButton from './CustomButton'
	
	export default {
		name: 'helpPanel',
		components: {
			customButton
		}
	}
</script>

<style scoped>
	.info-row {
		display: flex;
		align-items: center;
		height: 45px;
	}

	.p-right {
		padding-right: 10px;
	}
	
	.settings {
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 23px;
		height: 30px;
		width: 30px;
	}
	
	.info-text {
		margin-top: 3px;
	}
</style>
