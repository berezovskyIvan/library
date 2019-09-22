<template lang="pug">
  .row(@mouseover="isHover = true", @mouseout="isHover = false")
    input(type="file", @change="getPicture", style="display: none", :id="index")
    label.row__download-file(:for="index")
      span(style="margin-bottom: 3px") &#10152
    input(v-model="data.title", placeholder="Заголовок", maxlength="30")
    input(v-model="data.name", placeholder="Имя автора", maxlength="20")
    input(v-model="data.surname", placeholder="Фамилия автора", maxlength="20")
    input(v-model="data.pageCount", placeholder="Количество страниц", type="number", min="0", max="10000")
    input(v-show="options.publishing", v-model="data.publishing", placeholder="Издательство", maxlength="30")
    input(v-show="options.publicationYear", v-model="data.publicationYear", placeholder="Год публикации" type="number", min="1800")
    input(v-show="options.releaseDate", v-model="data.releaseDate", type="date", min="1800-01-01")
    img.row__cover(v-show="data.imagine && options.imagine", :src="data.imagine", accept="image/*")
    .row__add-button(v-show="isHover && data.imagine && options.imagine", @click="data.imagine = null")
      custom-button(diameter="20px", icon="&#10006", iconSize="15px", color="#e0e0e0")
    .row__buttons
      .row__buttons__container(@click="isValid && updateBooksData('update')")
        custom-button(v-show="isHover", diameter="25px", icon="&#10003", iconSize="21px", color="#00e676", :disabled="!isValid")
      .row__buttons__container(@click="updateBooksData('delete')")
        custom-button(v-show="isHover", diameter="25px", icon="&#10006", iconSize="18px", color="#ff3d00", @click="isValid && updateBooksData('delete')")
</template>

<script>
  import customButton from './customButton'

  export default {
    name: 'booksRowData',
    components: {
        customButton
    },
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
    }
  }
</script>

<style lang="less" scoped>
  .row {
    display: flex;
    align-items: center;
    height: 90px;
    padding-left: 10px;
    border-top: 1px solid #4dd0e1;

    input {
      margin: 0 10px 0 10px;
      height: 23px;
      width: 130px;
      border-width: 1px;
      border-radius: 3px;
    }

    &__download-file {
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

      &:hover {
        background: #e0e0e0;
      }
    }

    &__cover {
      max-height: 80%;
      padding-right: 5px;
    }

    &__buttons {
      position: absolute;
      display: flex;
      right: 20px;

      &__container {
        margin-right: 10px;
      }
    }
  }
</style>
