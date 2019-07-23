<template lang="pug">
	.row-block(@mouseover="isHover = true", @mouseout="isHover = false")
		input(v-model="bookData.title", placeholder="Заголовок", maxlength="30")
		input(v-model="bookData.name", placeholder="Имя автора", maxlength="20")
		input(v-model="bookData.surname", placeholder="Фамилия автора", maxlength="20")
		input(v-model="bookData.pageCount", placeholder="Количество страниц", type="number", min="0", max="10000")
		input(v-model="bookData.publishing", placeholder="Издательство", maxlength="30")
		input(v-model="bookData.publicationYear", placeholder="Год публикации" type="number", min="1800")
		input(v-model="bookData.releaseDate", type="date", min="1800-01-01")
		.row-button(v-show="isHover" style="background: #00e676")
			.icon.check &#10003
		.row-button(v-show="isHover", style="background: #ff3d00")
			.icon &#10006
</template>

<script>
	export default {
		name: 'booksRowData',
		data() {
			return {
				isHover: false,
				bookData: {
					title: '',
					name: '',
					surname: '',
					pageCount: null,
					publishing: '',
					publicationYear: null,
					releaseDate: ''
				}
			}
		},
		props: {
			data: {
				type: Object,
				default: {}
			}
		}
	}
</script>

<style scoped>
	.row-block {
		display: flex;
		align-items: center;
		height: 50px;
		border-top: 1px solid #4dd0e1;
	}
	
	.row-button {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 25px;
		width: 25px;
		margin-right: 10px;
		border-radius: 50%;
		cursor: pointer;
	}
	
	input {
		margin: 0 10px 0 10px;
		height: 23px;
		width: 150px;
		border-width: 1px;
		border-radius: 3px;
	}
	
	.icon {
		color: #fff;
	}

	.check {
		font-weight: bold;
	}
</style>
