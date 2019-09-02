<template lang="pug">
  label.position(@click="changeChecked")
    .box-border(:class="{ active: checked }")
      .checked-icon(v-if="checked") &#10003
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

<style scoped>
  .position {
    position: relative;
  }

  .box-border {
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

  .active {
    background: #e0e0e0 !important;
  }
</style>
