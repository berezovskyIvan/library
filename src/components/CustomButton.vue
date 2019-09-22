<template lang="pug">
  custom-tooltip(:value="tooltip")
    slot
      .button(:style="bloom", :class="{ 'button--disabled': disabled }")
        .button__icon(:style="{ fontSize: this.iconSize }", v-html="icon")
</template>

<script>
  import customTooltip from './customTooltip'

  export default {
    name: 'customButton',
    components: {
      customTooltip
    },
    props: {
      diameter: {
        type: String,
        default: '50px'
      },
      icon: {
        type: String,
        default: '&#43'
      },
      iconSize: {
        type: String,
        default: '60px',
      },
      color: {
        type: String,
        default: '#4dd0e1'
      },
      tooltip: {
        type: String,
        default: ''
      },
      disabled: {
        type: Boolean,
        default: false
      }
    },
    computed: {
      bloom: function() {
        return {
          height: this.diameter,
          width: this.diameter,
          background: this.color
        }
      }
    }
  }
</script>

<style lang="less" scoped>
  .button {
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    color: #fff;

    &:hover {
      cursor: pointer;
      opacity: 0.7;
    }

    &--disabled {
      background: #e0e0e0 !important;
      cursor: not-allowed !important;
    }

    &__icon {
      font-size: 60px;
      font-weight: bold;
      user-select: none;
    }    
  }
</style>
