<template lang="pug">
  .sort-block
    .title {{ title }}
    .sort-buttons
      .sort(style="align-items: flex-start", :class="{ active: activeSort === 'ASC' }", @click="sort('ASC')")
        .asc-sort &#10151
      .sort(style="align-items: flex-end", :class="{ active: activeSort === 'DESC' }", @click="sort('DESC')")
        .desc-sort &#10151
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

<style scoped>
  .sort-block {
    display: flex;
    width: 90px;
    height: 30px;
    border-radius: 6px;
    background: #eeeeee;
    padding-left: 5px;
  }

  .title {
    display: flex;
    align-items: center;
    height: 100%;
    width: 70%;
    font-size: 13px;
  }

  .sort-buttons {
    height: 100%;
    width: 30%;
  }

  .sort {
    display: flex;
    justify-content: center;
    height: 50%;
    width: 100%;
    font-size: 15px;
    cursor: pointer;
    color: #d7ccc8;
  }

  .asc-sort {
    transform: rotate(-90deg);
  }

  .desc-sort {
    transform: rotate(90deg);
    margin-left: 2px;
  }

  .active {
    color: #4dd0e1 !important;
  }
</style>
