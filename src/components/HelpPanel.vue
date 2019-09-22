<template lang="pug">
  .panel
    .panel__row
      .panel__row__icon.p-right &#9776
      .panel__row__text Открыть меню настроек
    .panel__row
      custom-button.p-right(diameter="30px", iconSize="35px")
      .panel__row__text Добавить книгу
    .panel__row
      custom-button.p-right(diameter="30px", iconSize="25px", icon="&#10003", color="#00e676")
      .panel__row__text Сохранить информацию о книге
    .panel__row
      custom-button.p-right(diameter="30px", iconSize="25px", icon="&#10003", color="#e0e0e0")
      .panel__row__text Введённая информация не валидна
    .panel__row
      custom-button.p-right(diameter="30px", iconSize="20px", icon="&#10006", color="#ff3d00")
      .panel__row__text Удалить информацию о книге
    .panel__row
      .panel__row__download &#10152
      .panel__row__text Загрузить обложку
    .panel__row
      img.p-right.panel__row__delete-book(src="../pictures/WarAndPeace.gif")
      custom-button.p-right(diameter="20px", icon="&#10006", iconSize="15px", color="#e0e0e0")
      .panel__row__text Удалить обложку
</template>

<script>
  import customButton from './customButton'

  export default {
    name: 'helpPanel',
    components: {
      customButton
    }
  }
</script>

<style lang="less" scoped>
  .panel {
    &__row {
      display: flex;
      align-items: center;
      height: 65px;
      
      &__icon {
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 23px;
        height: 30px;
        width: 30px;
      }

      &__text {
        margin-top: 3px;
      }

      &__download {
        font-size: 35px;
        transform: rotate(90deg);
        color: #4dd0e1;
      }

      &__delete-book {
        max-height: 65px;
      }
    }

    .p-right {
      padding-right: 10px;
    }
  }
</style>
