<template lang="pug">
  .container
    .side-panel(v-if="sPanel.isOpen")
      .side-panel__title
        .side-panel__title__button(@click="sPanel.isOpen = false") &#10006
      .side-panel__border
        settings-panel(v-show="sPanel.type === 'settings'", :options="options")
        help-panel(v-show="sPanel.type === 'help'")
    .header
      .header__button--settings(@click="sidePanelUse('settings')", :class="{ 'header__button--settings--open' : sPanel.isOpen && sPanel.type === 'settings' }") &#9776
      .header__button--help(@click="sidePanelUse('help')") &#63
      sort-block.header__sort--title(title="Заголовок", @sort="$event => sort($event, 'title')")
      sort-block.header__sort--year-public(title="Год публикации", @sort="$event => sort($event, 'publicationYear')")
      img.header__picture(src="./pictures/Books.png")
      span.header__title-text Добро пожаловать в веб библиотеку
      .header__msg(:class="{ 'header__msg--active': msg.active }") {{ msg.text }}
        span.header__msg__exclamation(:style="bloom") &#33
    books-row-data(v-for="(item, index) in booksData", :data="item", :index="index", :options="options", @updateBooksData="updateBooksData")
    .button-block(@click="addBookData")
      custom-button(diameter="70px", tooltip="Добавить")
</template>

<script>
  import settingsPanel from './components/settingsPanel'
  import helpPanel from './components/helpPanel'
  import booksRowData from './components/booksRowData'
  import customButton from './components/customButton'
  import sortBlock from './components/sortBlock'

  export default {
    name: 'library',
    components: {
      settingsPanel,
      helpPanel,
      booksRowData,
      customButton,
      sortBlock
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
        msg: {
          active: false,
          text: ''
        }
      }
    },
    computed: {
      bloom: function () {
        return {
          color: this.msg.text === 'Запись сохранена' ? '#00e676' : '#ff3d00'
        }
      }
    },
    watch: {
      'options.publishing': function() { this.saveLocalStorage('options', this.options) },
      'options.publicationYear': function() { this.saveLocalStorage('options', this.options) },
      'options.releaseDate': function() { this.saveLocalStorage('options', this.options) },
      'options.imagine': function() { this.saveLocalStorage('options', this.options) }
    },
    methods: {
      sidePanelUse(type) {
        this.sPanel.isOpen = !this.sPanel.isOpen || this.sPanel.type !== type
        this.sPanel.type = this.sPanel.isOpen ? type : ''
      },
      getArrayClone(arr) {
        return JSON.parse(JSON.stringify(arr))
      },
      getBooksData() {
        const storageData = JSON.parse(localStorage.getItem('booksData'))

        if (storageData && storageData.length) {
          this.cloud = storageData
          this.booksData = this.getArrayClone(this.cloud)
        } else {
          this.addBookData()
        }
      },
      getOptions() {
        const options = JSON.parse(localStorage.getItem('options'))

        if (options) { this.options = options }
      },
      saveLocalStorage(name, data) {
        localStorage.setItem(name, JSON.stringify(data))
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

        this.booksData.push(obj)
      },
      updateBooksData({ type, index, data }) {
        if (type === 'update') {
          this.cloud[index] = data
          this.msg.text = 'Запись сохранена'
        } else {
          this.cloud.splice(index, 1)
          this.booksData.splice(index, 1)
          this.msg.text = 'Запись удалена'
        }

        this.saveLocalStorage('booksData', this.cloud)

        this.msg.active = true

        setTimeout(() => {
          this.msg.active = false
        }, 2000)
      },
      sort($event, name) {
        const sortType = $event.type === 'ASC' ? 1 : -1
        this.cloud.sort((a, b) => { return a[name] > b[name] ? sortType : -sortType })
        this.booksData.sort((a, b) => { return a[name] > b[name] ? sortType : -sortType })
        localStorage.setItem('booksData', JSON.stringify(this.cloud))
      }
    },
    mounted() {
      this.getOptions()
      this.getBooksData()
    }
  }
</script>

<style lang="less" scoped>
  @keyframes carousel {
    from {
      right: 0;
      visibility: visible;
    }
    to {
      right: 50px;
    }
  }

  .container {
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

    &__title {
      height: 50px;

      &__button {
        display: flex;
        align-items: center;
        justify-content: center;
        position: absolute;
        top: 5px;
        left: 5px;
        height: 30px;
        width: 30px;
        font-size: 17px;
        border-radius: 50%;
        cursor: pointer;
        
        &:hover {
          background-color: #e0e0e0;
        }
      }
    }

    &__border {
      padding: 10px;
    }
  }

  .header {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 70px;

    &__button {
      &--settings, &--help {
        display: flex;
        align-items: center;
        justify-content: center;
        position: absolute;
        width: 35px;
        height: 35px;
        border-radius: 50%;
        cursor: pointer;

        &:hover {
          background: #e0e0e0;
        }
      }

      &--settings {
        left: 15px;
        font-size: 23px;
        transition: 0.5s;

         &--open {
          transform: rotate(90deg);
          transition: 0.5s;
        }
      }

      &--help {
        left: 60px;
        margin-top: 2px;
        font-size: 28px;
      }
    }

    &__sort {
      &--title, &--year-public {
        position: absolute;
      }

      &--title {
        left: 130px;
      }

      &--year-public {
        left: 240px;
      }
    }

    &__picture {
      width: 50px;
      height: 50px;
      padding-right: 10px;
    }

    &__title-text {
      font-size: 23px;
      font-weight: 550;
    }
    
    &__msg {
      z-index: 2;
      position: absolute;
      display: flex;
      visibility: hidden;
      align-items: center;
      justify-content: center;
      height: 40px;
      width: 150px;
      font-size: 15px;
      border: 1px solid #90a4ae;
      border-radius: 4px;

      &--active {
        animation: carousel 2s;
      }

      &__exclamation {
        left: 10px;
        padding-left: 5px;
        font-size: 30px;
        font-weight: bold;
      }
    }
  }

  .button-block {
    position: fixed;
    bottom: 15px;
    right: 15px;
  }
</style>
