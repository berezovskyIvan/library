<template lang="pug">
	.row-block(@mouseover="isHover = true", @mouseout="isHover = false")
		input(type="file", @change="getPicture", style="display: none", :id="index")
		label.download-file(:for="index")
			span(style="margin-bottom: 3px") &#10152
		input(v-model="data.title", placeholder="Заголовок", maxlength="30")
		input(v-model="data.name", placeholder="Имя автора", maxlength="20")
		input(v-model="data.surname", placeholder="Фамилия автора", maxlength="20")
		input(v-model="data.pageCount", placeholder="Количество страниц", type="number", min="0", max="10000")
		input(v-show="options.publishing", v-model="data.publishing", placeholder="Издательство", maxlength="30")
		input(v-show="options.publicationYear", v-model="data.publicationYear", placeholder="Год публикации" type="number", min="1800")
		input(v-show="options.releaseDate", v-model="data.releaseDate", type="date", min="1800-01-01")
		img.cover(v-show="data.imagine && options.imagine", :src="data.imagine", accept="image/*")
		.delete-cover(v-show="isHover && data.imagine && options.imagine", @click="data.imagine = null") &#10006
		.buttons-block
			.row-button(v-show="isHover", style="background: #00e676", :class="{ disabled : !isValid }", @click="isValid && updateBooksData('update')")
				.icon.check &#10003
			.row-button(v-show="isHover", style="background: #ff3d00", @click="updateBooksData('delete')")
				.icon &#10006
</template>

<script>
	export default {
		name: 'booksRowData',
		data() {
			return {
				isHover: false
			}
		},
		props: {
			data: {
				type: Object,
				default: {}
			},
            index: {
                type: Number,
                default: 0
            },
            options: {
				type: Object,
                default: null
            }
		},
        computed: {
            isValid: function () {
                return this.data.title && this.data.title.length <= 30 &&
                this.data.name && this.data.name.length <= 20 &&
                this.data.surname && this.data.surname.length <= 20 &&
                this.data.pageCount > 0 && this.data.pageCount <= 10000 &&
                this.data.publishing && this.data.publishing.length <= 30 &&
                this.data.publicationYear >= 1800 &&
                this.data.releaseDate >= '1800-01-01'
            }
        },
        methods: {
            getPicture(file) {
            	if (file.target.files.length) {
                    const reader = new FileReader()

                    reader.onload = ($event) => {
                        this.data.imagine = $event.target.result
                    }

                    reader.readAsDataURL(file.target.files[0])
                }
            },
            updateBooksData(type) {
                this.$emit('updateBooksData', {
                	type,
                    index: this.index,
                    data: this.data
                })
            }
        },
        mounted() {

        }
    }
</script>

<style scoped>
	.row-block {
		display: flex;
		align-items: center;
		height: 70px;
        padding-left: 10px;
		border-top: 1px solid #4dd0e1;
	}

    .buttons-block {
        position: absolute;
        display: flex;
        right: 20px;
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
		width: 130px;
		border-width: 1px;
		border-radius: 3px;
	}

	.icon {
		color: #fff;
	}

	.check {
		font-weight: bold;
	}

    .disabled {
        background: #e0e0e0 !important;
        cursor: not-allowed;
    }

    .cover {
        height: 50px;
        width: 50px;
        padding-right: 5px;
    }

    .delete-cover {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 20px;
        width: 20px;
        font-size: 15px;
        border-radius: 50%;
        color: #fff;
        background: #e0e0e0;
        cursor: pointer;
    }

    .download-file {
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 30px;
        transform: rotate(90deg);
        color: #4dd0e1;
        height: 35px;
        width: 35px;
        border-radius: 50%;
        cursor: pointer;
    }

    .download-file:hover {
        background: #e0e0e0;
    }
</style>
