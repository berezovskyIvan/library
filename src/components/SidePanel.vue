<template lang="pug">
	.side-panel
		.close-button(@click="closeSidePanel") &#10006
</template>

<script>
	export default {
		name: 'sidePanel',
        methods: {
			closeSidePanel() {
				this.$emit('closeSidePanel')
            }
        }
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

    .close-button {
        display: flex;
        align-items: center;
        justify-content: center;
        position: absolute;
        top: 5px;
        left: 5px;
        height: 30px;
        width: 30px;
        border-radius: 50%;
        cursor: pointer;
    }

    .close-button:hover {
        background-color: #e0e0e0;
    }
</style>
