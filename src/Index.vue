<template lang="pug">
	.page-block
		side-panel(v-if="sidePanelOpen", @closeSidePanel="sidePanelOpen = false")
		.header
			.settings(@click="sidePanelOpen = !sidePanelOpen") &#9783
			div Welcome to the web library
		books-row-data.row-block(v-for="item in booksData", :data="item")
		.button-block(@click="addBookData")
			custom-button(diameter="70px")
</template>

<script>
	import sidePanel from './components/SidePanel'
	import booksRowData from './components/BooksRowData'
	import customButton from './components/CustomButton'
	import customTooltip from './components/customTooltip'

	export default {
		name: 'library',
		components: {
			sidePanel,
			booksRowData,
			customButton,
			customTooltip
		},
		data() {
			return {
				sidePanelOpen: false,
				booksData: [
					{
						title: 'Война и мир',
						name: 'Лев',
						surname: 'Толстой',
						pageCount: 1500,
						publishing: 'РОСМЭН',
						publicationYear: 1900,
						releaseDate: '1988-01-01'
					}
				]
			}
		},
		methods: {
			addBookData() {
				this.booksData.push({
					title: '',
					name: '',
					surname: '',
					pageCount: null,
					publishing: '',
					publicationYear: null,
					releaseDate: null
				})
			}
		}
	}
</script>

<style scoped>
	.page-block {
		height: 100%;
	}

	.header {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 60px;
		font-size: 23px;
		font-weight: 550;
	}

	.settings {
		display: flex;
		align-items: center;
		justify-content: center;
		position: absolute;
		width: 35px;
		height: 35px;
		left: 10px;
		border-radius: 50%;
		cursor: pointer;
	}

	.settings:hover {
		background: #e0e0e0;
	}

	.button-block {
		position: fixed;
		bottom: 15px;
		right: 15px;
	}
</style>
