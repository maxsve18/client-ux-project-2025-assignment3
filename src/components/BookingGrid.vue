<template>
  <div class="booking-grid">
    <div class="booking-row" v-for="worker in groupedBookings" :key="days[0]?.date">
      <div class="booking-cells">
        <div v-for="(booking, index) in days"
             :key="index"
             class="booking-cell"
             :class="getClass(booking.type)"
             :title="`${booking.date}: ${booking.type}`">
          <img :src="getStatusIcon(booking.type, booking.extent)" class="status-icon" alt="status-svg"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {computed} from 'vue'
import {format, eachDayOfInterval, isWeekend} from 'date-fns'

const props = defineProps({
  bookings: Array,
  selectedType: String,
  selectedWorker: String,
})

// Generate all workdays for the whole year
function generateAllWorkdays() {
  return eachDayOfInterval({
    start: new Date(2025, 0, 1),
    end: new Date(2025, 11, 31),
  })
      .filter(date => !isWeekend(date))
      .map(date => format(date, "yyyy-MM-dd"))
}

const allDates = generateAllWorkdays()


const groupedBookings = computed(() => {
  //If bookings undefined return an empty array.
  if (!props.bookings) {
    return [];
  }

  const map = new Map()
  const bookingMap = {}
  props.bookings.forEach((b) => {
    if (
        (!props.selectedWorker || b.worker === props.selectedWorker) &&
        (!props.selectedType || b.type === props.selectedType)
    ) {
      const key = `${b.worker}_${b.date}`
      bookingMap[key] = b
    }
  })

  const days = allDates.map((date) => {
    const dayData = [];
    const workers = new Set(props.bookings.map((b) => b.worker));
    workers.forEach((worker) => {
      const key = `${worker}_${date}`;
      if (bookingMap[key]) {
        dayData.push({
          date,
          type: bookingMap[key].type,
          extent: bookingMap[key].extent || 0,
          worker: worker, // Include worker in the day's data
        });
      } else {
        dayData.push({date, type: "Tillganglig", extent: 0, worker: worker}); // Include worker
      }
    });
    return dayData;
  });

  return days;
});

function getClass(type) {
  const map = {
    Tillganglig: 'available',
    Franvaro: 'absence',
    Bokad: 'fullybooked',
    Bokad50: 'booked-half',
    Pre: 'pre-booked',
    Pre50: 'pre-booked-half',
  }
  return map[type] || ''
}

function getStatusIcon(type, extent) {
  const basePath = new URL('../assets/status', import.meta.url).href
  if (type === 'Franvaro') return `${basePath}/absence.svg}`
  if (type === 'Tillganglig') return `${basePath}/available.svg}`
  if (type === 'Bokad' && extent === 100) return `${basePath}/booked100.svg}`
  if (type === 'Bokad' && extent === 50) return `${basePath}/booked50.svg}`
  if (type === 'Pre' && extent === 100) return `${basePath}/pre100.svg}`
  if (type === 'Pre' && extent === 50) return `${basePath}/pre50.svg}`
  return ''
}
</script>

<style scoped>
.booking-grid {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.booking-row {
  display: flex;
  align-items: center;
}

.worker-name {
  width: 180px;
  font-weight: bold;
}

.booking-cells {
  display: flex;
}

.booking-cell {
  width: 20px;
  height: 20px;
  margin: 2px;
  border-radius: 4px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.status-icon {
  width: 100%;
  height: 100%;
}
</style>