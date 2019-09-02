<template lang="pug">
  div
    .info-row
      .settings.p-right &#9776
      .info-text Открыть меню настроек
    .info-row
      custom-button.p-right(diameter="30px", iconSize="35px")
      .info-text Добавить книгу
    .info-row
      custom-button.p-right(diameter="30px", iconSize="25px", icon="&#10003", color="#00e676")
      .info-text Сохранить информацию о книге
    .info-row
      custom-button.p-right(diameter="30px", iconSize="25px", icon="&#10003", color="#e0e0e0")
      .info-text Введённая информация не валидна
    .info-row
      custom-button.p-right(diameter="30px", iconSize="20px", icon="&#10006", color="#ff3d00")
      .info-text Удалить информацию о книге
    .info-row
      .download &#10152
      .info-text Загрузить обложку
    .info-row
      img.p-right.delete-book(src="../pictures/WarAndPeace.gif")
      custom-button.p-right(diameter="20px", icon="&#10006", iconSize="15px", color="#e0e0e0")
      .info-text Удалить обложку
</template>

<script>
  import customButton from './CustomButton'

  export default {
    name: 'helpPanel',
    components: {
      customButton
    }
  }
</script>

<style scoped>
  .info-row {
    display: flex;
    align-items: center;
    height: 65px;
  }

  .p-right {
    padding-right: 10px;
  }

  .settings {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 23px;
    height: 30px;
    width: 30px;
  }

  .info-text {
    margin-top: 3px;
  }

  .download {
    font-size: 35px;
    transform: rotate(90deg);
    color: #4dd0e1;
  }

  .delete-book {
    max-height: 65px;
  }
</style>
