<template lang="pug">
  label.checkbox(@click="changeChecked")
    .checkbox__border(:class="{ checked }")
      .checkbox__border__icon(v-if="checked") &#10003
</template>

<script>
  export default {
    name: 'customCheckBox',
    props: {
      checked: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      changeChecked() {
        this.$emit('changeChecked', this.checked)
      }
    }
  }
</script>

<style lang="less" scoped>
  .checkbox {
    position: relative;

    .checked {
      background: #e0e0e0 !important;
    }

    &__border {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 17px;
      width: 17px;
      border-radius: 3px;
      border: 2px solid #e0e0e0;
      background-color: #fff;
      cursor: pointer;
      user-select: none;
    } 
  }
</style>
