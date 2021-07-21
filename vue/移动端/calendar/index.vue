<template>
  <div class="wapper">
    <MonthSelector v-model="month" />
    <div class="day-list">
      <span v-for="(day, index) in dayList" :key="index">{{ day }}</span>
    </div>
    <DateList :month="month" :dateList="monthDateList" />
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, reactive } from 'vue'
import MonthSelector from './components/monthSelector.vue'
import DateList from './components/dateList.vue'
import { DateItem } from './type'

export default defineComponent({
  components: {
    MonthSelector,
    DateList
  },
  setup() {
    const date = new Date()
    const month = ref(date.getMonth() + 1)
    date.setDate(1)
    const yaer = date.getFullYear()
    const monthDateList: DateItem[][] = reactive(
      Array.from(Array(12), (data, index) => {
        date.setMonth(index + 1)
        date.setDate(0)
        const lastDate = date.getDate()
        const lastDay = date.getDay()
        const lastDateList: DateItem[] = Array.from(
          Array(6 - lastDay),
          (data, index) => {
            return {
              cls: 'disable',
              value: index + 1
            }
          }
        )

        date.setDate(1)
        const firstDate = date.getDate()
        const firstDay = date.getDay()
        date.setDate(0)
        const preMonthLastDate = date.getDate()
        const diff = firstDay
        const fristDateList: DateItem[] = Array.from(
          Array(diff),
          (data, index) => {
            return {
              cls: 'disable',
              value: preMonthLastDate - (diff - 1 - index)
            }
          }
        )

        const dateList: DateItem[] = Array.from(
          Array(lastDate - firstDate + 1),
          (data, index) => {
            return {
              cls: 'normal',
              value: index + 1
            }
          }
        )

        // 1月前一个月是上一年，所以要设回当前年份
        date.setFullYear(yaer)
        date.setDate(1)
        return fristDateList.concat(dateList).concat(lastDateList)
      })
    )
    const dayList = ['日', '一', '二', '三', '四', '五', '六']
    return {
      month,
      dayList,
      monthDateList
    }
  }
})
</script>
<style scoped>
.wapper {
  display: flex;
  flex-direction: column;
  width: 300px;
  text-align: center;
  overflow: hidden;
}
.day-list {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  row-gap: 20px;
  font-size: 16px;
  font-weight: 500;
  color: #888888;
  margin-top: 16px;
  padding-bottom: 16px;
  margin-bottom: 20px;
  border-bottom: 1px solid #e5e5e5;
}
</style>
