<template>
  <div class="month-wapper">
    <span :class="leftCls" @click="handleChangeMonth(-1)" />
    <span class="month">{{ modelValue }}月</span>
    <span :class="rightCls" @click="handleChangeMonth(1)" />
  </div>
</template>
<script lang="ts">
import { defineComponent, computed } from 'vue'
const props = {
  modelValue: {
    type: Number,
    default: 1,
    validator: function (value: number) {
      return value <= 12 && value >= 1
    }
  }
}
export default defineComponent({
  name: 'MonthSelector',
  props: props,
  emits: ['update:modelValue'],
  setup(props, context) {
    const leftCls = computed(() => {
      const value = props.modelValue
      return 'arrow left ' + (value === 1 ? 'disabled' : '')
    })
    const rightCls = computed(() => {
      const value = props.modelValue
      return 'arrow ' + (value === 12 ? 'disabled' : '')
    })

    const handleChangeMonth = (val: number) => {
      const value = props.modelValue
      val = value + val
      if (val <= 12 && val >= 1) {
        context.emit('update:modelValue', val)
      }
    }

    return {
      leftCls,
      rightCls,
      handleChangeMonth
    }
  }
})
</script>
<style scoped>
.month-wapper {
  align-items: center;
  justify-content: center;
  font-size: 20px;
  font-weight: 800;
  color: #000000;
  display: flex;
  user-select: none;
}
.arrow {
  height: 0px;
  width: 0px;
  border-top: 10px solid transparent;
  border-left: 10px solid #000000;
  border-bottom: 10px solid transparent;
  cursor: pointer;
}
.disabled {
  border-left: 10px solid #888888;
}
.left {
  transform: rotate(180deg);
}
.month {
  margin-right: 48px;
  margin-left: 48px;
  width: 48px;
  text-align: center;
}
</style>
