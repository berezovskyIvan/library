<template lang="pug">
  .sort
    .sort__title {{ title }}
    .sort__buttons
      .sort__buttons__icon(style="align-items: flex-start", :class="{ active: activeSort === 'ASC' }", @click="sort('ASC')")
        .sort__buttons__icon--asc &#10151
      .sort__buttons__icon(style="align-items: flex-end", :class="{ active: activeSort === 'DESC' }", @click="sort('DESC')")
        .sort__buttons__icon--desc &#10151
</template>

<script>
  export default {
    name: 'sortBlock',
    data() {
      return {
        activeSort: ''
      }
    },
    props: {
      title: {
        type: String,
        default: ''
      }
    },
    methods: {
      sort(type) {
        this.activeSort = type
        this.$emit('sort', { type })
      }
    }
  }
</script>

<style lang="less" scoped>
  .sort {
    display: flex;
    width: 90px;
    height: 30px;
    border-radius: 6px;
    background: #eeeeee;
    padding-left: 5px;

    &__title {
      display: flex;
      align-items: center;
      height: 100%;
      width: 70%;
      font-size: 13px;
    }

    &__buttons {
      height: 100%;
      width: 30%;

      .active {
        color: #4dd0e1 !important;
      }

      &__icon {
        display: flex;
        justify-content: center;
        height: 50%;
        width: 100%;
        font-size: 15px;
        cursor: pointer;
        color: #d7ccc8;
        
        &--asc {
          transform: rotate(-90deg);
        }

        &--desc {
          transform: rotate(90deg);
          margin-left: 2px;
        }
      }
    }
  }
</style>
