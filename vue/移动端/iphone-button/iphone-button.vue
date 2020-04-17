<template>
  <div class="iphone-button"
  :style="{ '--height': `${height}px`, '--width': `${width}px`, '--padding': `${padding}px` }">
    <input type="checkbox" class="circular" @click="onClick">
  </div>
</template>

<script>
export default {
  name: 'IphoneButton',
  props: {
    height: {
      default: 62,
      type: Number
    },
    width: {
      default: 102,
      type: Number
    },
    padding: {
      default: 4,
      type: Number
    }
  },
  data () {
    return {
      isClick: false
    }
  },
  methods: {
    onClick () {
      this.isClick = !this.isClick
      if (this.isClick) {
        this.$emit('on-select')
      } else {
        this.$emit('on-cancel')
      }
    }
  }
}
</script>

<style lang="less" scoped>
@import './iphone-button.less';
</style>
