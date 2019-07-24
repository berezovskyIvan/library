<template lang="pug">
	.page-block
		.side-panel(v-if="sPanel.isOpen")
			.title
				.close-button(@click="sPanel.isOpen = false") &#10006
			.main
				settings-panel(v-show="sPanel.type === 'settings'", :options="options")
				help-panel(v-show="sPanel.type === 'help'")
		.header
			.options-button.settings(@click="sidePanelUse('settings')", :class="{ 'side-panel-open' : sPanel.isOpen && sPanel.type === 'settings' }") &#9776
			.options-button.help(@click="sidePanelUse('help')") &#63
			img.books-picture(src="./pictures/Books.png")
			span.title-text Добро пожаловать в веб библиотеку
			.message(v-show="message.visibility") {{ message.text }}
				span.exclamation(:style="bloom") &#33
		books-row-data.row-block(v-for="(item, index) in booksData", :data="item", :index="index", :options="options", @updateBooksData="updateBooksData")
		.button-block(@click="addBookData")
			custom-button(diameter="70px")
</template>

<script>
	import settingsPanel from './components/SettingsPanel'
	import helpPanel from './components/HelpPanel'
	import booksRowData from './components/BooksRowData'
	import customButton from './components/CustomButton'
	import customTooltip from './components/customTooltip'

	export default {
		name: 'library',
		components: {
			settingsPanel,
			helpPanel,
			booksRowData,
			customButton,
			customTooltip
		},
		data() {
			return {
				sPanel: {
					isOpen: false,
					type: ''
				},
                options: {
                    publishing: true,
                    publicationYear: true,
                    releaseDate: true,
                    imagine: true
                },
                cloud: [],
				booksData: [],
                message: {
				    visibility: false,
                    text: ''
                }
			}
		},
        computed: {
            bloom: function () {
                return {
                	color: this.message.text === 'Запись сохранена' ? '#00e676' : '#ff3d00'
                }
            }
        },
		methods: {
			sidePanelUse(type) {
				this.sPanel.isOpen = !this.sPanel.isOpen || this.sPanel.type !== type
				this.sPanel.type = this.sPanel.isOpen ? type : ''
			},
			getArrayClone(arr) {
			    return JSON.parse(JSON.stringify(arr))
            },
			addBookData() {
				const obj = {
                    title: '',
                    name: '',
                    surname: '',
                    pageCount: null,
                    publishing: '',
                    publicationYear: null,
                    releaseDate: null,
                    imagine: null
                }

                this.cloud.push(obj)
				this.booksData.push(obj)
			},
            updateBooksData({ type, index, data }) {
                if (type === 'update') {
                	this.cloud[index] = data
                    this.message.text = 'Запись сохранена'
                } else {
                	this.cloud.splice(index, 1)
                    this.booksData.splice(index, 1)
                    this.message.text = 'Запись удалена'
                }

                localStorage.setItem('booksData', JSON.stringify(this.cloud))

                this.message.visibility = true

                setTimeout(() => {
                	this.message.visibility = false
                }, 2000)
            }
		},
        mounted() {
			const storageData = JSON.parse(localStorage.getItem('booksData'))

            if (storageData && storageData.length) {
            	this.cloud = storageData
                this.booksData = this.getArrayClone(this.cloud)
            } else {
            	console.log('fuck')
              this.addBookData()
            }
        }
	}
</script>

<style scoped>
    @keyframes carousel {
        0% {
            right: 0px;
        }
        10% {
            right: 5px;
        }
        20% {
            right: 10px;
        }
        30% {
            right: 15px;
        }
        40% {
            right: 20px;
        }
        50% {
            right: 25px;
        }
        60% {
            right: 30px;
        }
        70% {
            right: 35px;
        }
        80% {
            right: 40px;
        }
        90% {
            right: 45px;
        }
        100% {
            right: 50px;
        }
    }

	.page-block {
		height: 100%;
        border-bottom: 1px solid #4dd0e1;
	}

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
	
    .title {
        height: 50px;
    }

    .main {
        padding: 10px;
    }
	
	.header {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 70px;
	}

    .title-text {
        font-size: 23px;
        font-weight: 550;
    }

    .books-picture {
        width: 50px;
        height: 50px;
        padding-right: 10px;
    }

	.options-button {
		display: flex;
		align-items: center;
		justify-content: center;
		position: absolute;
		width: 35px;
		height: 35px;
		border-radius: 50%;
		cursor: pointer;
	}

	.options-button:hover {
		background: #e0e0e0;
	}

	.settings {
		left: 15px;
		font-size: 23px;
		transition: 0.5s;
	}
	
	.help {
		left: 60px;
		margin-top: 2px;
		font-size: 28px;
	}
	
    .side-panel-open {
        transform: rotate(90deg);
        transition: 0.5s;
    }

	.button-block {
		position: fixed;
		bottom: 15px;
		right: 15px;
	}

    .message {
        z-index: 2;
        position: absolute;
        display: flex;
        align-items: center;
        justify-content: center;
        height: 40px;
        width: 150px;
        right: 50px;
        font-size: 15px;
        border: 1px solid #90a4ae;
        border-radius: 4px;
        animation: carousel 0.5s;
    }

    .exclamation {
        left: 10px;
        padding-left: 5px;
        font-size: 30px;
        font-weight: bold;
    }
</style>
