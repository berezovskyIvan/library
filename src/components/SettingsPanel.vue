<template lang="pug">
  div
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

<style scoped>
  .option-row {
    display: flex;
    align-items: center;
    height: 40px;
  }

  span {
    margin-left: 10px;
  }
</style>
