<template>
  <div
    class="date-list-wapper"
    :style="{ transform: `translateX(calc((-300px * ${month - 1}))` }"
  >
    <div class="date-grid" v-for="(dl, month) in dateList" :key="month">
      <div v-for="(date, index) in dl" :key="index" :class="date.cls">
        <span>{{ date.value }}</span>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, PropType } from 'vue'
import { DateItem } from '../type'
const props = {
  dateList: {
    type: Array as PropType<DateItem[][]>,
    default: () => []
  },
  month: {
    tpye: Number,
    default: new Date().getMonth() + 1
  }
}
export default defineComponent({
  props: props
})
</script>
<style scoped>
.date-list-wapper {
  display: flex;
  transition: all 0.3s;
  flex-wrap: nowrap;
}
.date-grid {
  display: grid;
  flex-shrink: 0;
  width: 300px;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  row-gap: 20px;
  font-size: 16px;
  font-weight: 800;
  text-align: center;
}
.disable {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #aaaaaa;
}
.normal {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #000000;
}
</style>
