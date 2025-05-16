<template>
 <div class="month-view">
   <div v-for="week in weeksOfMonth" :key="week.weekNumber" class="week-block" >
     <div class="week-number">Vecka {{ week.weekNumber }}</div>
     <div class="week-days">
       <div v-for="day in week.days" :key="day.date.toISOString()" class="day-box">
          <div class="day-label"> {{ day.label }} </div>
          <div class="day-number">{{ day.date.getDate() }}</div>
      </div>
    </div>
   </div>
 </div>
</template>

<script setup>
import { computed } from 'vue'
const props = defineProps ({
  startDate: Date,
  endDate: Date,
})

const weekLabels = ["M", "T", "O", "T", "F"]
function getWeekNumber(date) {
  const data = new Date(Date.UTC(date.getFullYear(),date.getMonth(), date.getDate()))
  data.setUTCDate(data.getUTCDate() + 4 - (data.getUTCDay() || 7))
  const yearStart = new Date (Date.UTC(data.getUTCFullYear(), 0, 1))
  const weekNo = Math.ceil((((data -yearStart) / 86400000) + 1) / 7)
  return weekNo
}

function cloneDate(date) {
  return new Date(date.getTime())
}
const weeksOfMonth = computed(() => {
  const result = []

  // Flytta current till måndag i startveckan
  let current = new Date(props.startDate)
  current.setDate(current.getDate() - ((current.getDay() + 6) % 7))

  // Generera alltid 4 veckor
  for (let weekIndex = 0; weekIndex < 4; weekIndex++) {
    const weekStart = cloneDate(current)
    const days = []

    for (let i = 0; i < 5; i++) {
      const day = new Date(weekStart)
      day.setDate(weekStart.getDate() + i)

      days.push({
        label: weekLabels[i],
        date: day
      })
    }

    result.push({
      weekNumber: getWeekNumber(weekStart),
      days
    })

    current.setDate(current.getDate() + 7)
  }

  return result
})

</script>

<style scoped>
.month-view {
  display: flex;
  flex-direction: row;

}

.week-block {
  display: flex;
  flex-direction: column;
}

.week-days {
  display: flex;
  border: 1px solid #555555;
  padding: 10px 29px 10px 25px;
}

.week-number {
  font-weight: 600;
  font-size: 18px;
  padding-bottom: 30px;
  text-align: left;
}

.day-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 40px;
  cursor: pointer;
}

.day-label {
  font-weight: bold;
  font-size: 18px;
}

.day-number {
  font-size: 12px;
  color: #555;
}
</style>
