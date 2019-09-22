<template lang="pug">
  .panel
    .panel__row
      custom-check-box(:checked="options.publishing", @changeChecked="options.publishing = !options.publishing")
      span Издательство
    .panel__row
      custom-check-box(:checked="options.publicationYear", @changeChecked="options.publicationYear = !options.publicationYear")
      span Год публикации
    .panel__row
      custom-check-box(:checked="options.releaseDate", @changeChecked="options.releaseDate = !options.releaseDate")
      span Дата выхода
    .panel__row
      custom-check-box(:checked="options.imagine", @changeChecked="options.imagine = !options.imagine")
      span Обложка
</template>

<script>
  import customCheckBox from './customCheckBox'

  export default {
    name: 'settingsPanel',
    components: {
      customCheckBox
    },
    props: {
      options: {
        type: Object,
        default: {}
      }
    }
  }
</script>

<style lang="less" scoped>
  .panel {
    &__row {
      display: flex;
      align-items: center;
      height: 40px;
    }

    span {
      margin-left: 10px;
    }
  }
</style>
