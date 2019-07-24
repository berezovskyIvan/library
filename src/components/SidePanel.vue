<template lang="pug">
	.side-panel
		.title
			.close-button(@click="closeSidePanel") &#10006
		.main
			.option-row
				custom-check-box(:checked="options.publishing", @changeChecked="options.publishing = !options.publishing")
				span Издательство
			.option-row
				custom-check-box(:checked="options.publicationYear", @changeChecked="options.publicationYear = !options.publicationYear")
				span Год публикации
			.option-row
				custom-check-box(:checked="options.releaseDate", @changeChecked="options.releaseDate = !options.releaseDate")
				span Дата выхода
			.option-row
				custom-check-box(:checked="options.imagine", @changeChecked="options.imagine = !options.imagine")
				span Обложка
</template>

<script>
    import customCheckBox from './CustomCheckBox'

	export default {
		name: 'sidePanel',
        components: {
		    customCheckBox
        },
        props: {
			options: {
				type: Object,
                default: {}
            }
        },
        methods: {
			closeSidePanel() {
				this.$emit('closeSidePanel')
            }
        }
	}
</script>

<style scoped>
	.side-panel {
        z-index: 1;
		position: absolute;
		height: 100%;
		width: 350px;
		top: 0;
		right: 0;
		border-left: 1px solid #4dd0e1;
		background: #fff;
	}

    .title {
        height: 50px;
    }

    .main {
        padding: 10px;
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
        font-size: 20px;
        border-radius: 50%;
        cursor: pointer;
    }

    .close-button:hover {
        background-color: #e0e0e0;
    }

    .option-row {
        display: flex;
        align-items: center;
        height: 40px;
    }

    span {
        margin-left: 10px;
    }
</style>
