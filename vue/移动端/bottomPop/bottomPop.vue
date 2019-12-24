<template>
  <div class="bottomBox" :style="{ 'z-index': showBottom ? '2' : '-1'}">
    <div class="mask" :style="{ 'opacity': opacity}" @tap="onClose"></div>
    <div class="boxContent" :style="{ 'transform': `translateY(${translateY}%)` }">
      <slot name="content"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BoomPop',
  props: {
    showBottom: {
      default: false,
      type: Boolean
    }
  },
  watch: {
    showBottom () {
      if (this.showBottom) {
        this.translateY = 0
        this.opacity = 0.6
      }
    }
  },
  data () {
    return {
      translateY: 100,
      opacity: 0,
    }
  },
  methods: {
    onClose () {
      this.translateY = 100
      this.opacity = 0
      setTimeout(() => {
        this.$emit('on-close')
      }, 300)
    } 
  }
}
</script>

<style lang="less" scoped>
.bottomBox{
  position: fixed;
  width: 100vw;
  .mask{
    position: fixed;
    top: 0px;
    left: 0px;
    height: 100vh;
    width: 100vw;
    transition: all 0.3s;
    background: rgb(0, 0, 0, 0.6);
  }
  .boxContent{
    position: fixed;
    width: 100%;
    background: white;
    bottom: 0px;
    transition: all 0.3s;
  }
}
</style>
