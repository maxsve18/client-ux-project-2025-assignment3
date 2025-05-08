<template>
<div class="booking-grid">
  <div class="booking-row" v-for="worker in groupedBookings" :key="worker.name">
    <div class="worker-name">{{ worker.name }}</div>
    <div class="booking-cells">
    <div v-for="(booking, index) in worker.days"
         :key="index"
         class="booking-cell"
         :class="getClass(booking.type)"
         :title="`${booking.date}: ${booking.type}`">
    </div>
    </div>
  </div>
</div>
</template>

<script setup>
import { computed } from 'vue'

defineProps ({
  bookings: Array,
  selectedType: String,
  SelectedWorker: String,
})

const groupedBookings = computed(() => {
  const map = new Map()
  bookings.forEach((b) => {
    if (
        (!selectedWorker || b.worker === selectedWorker) &&
        (!selectedType || b.type === selectedType)
    ) {
      if (!map.has(b.worker)) {
        map.set(b.worker, [])
      }
      map.get(b.worker).push({
        date: b.date,
        type: b.type,
      })
    }
  })

  return Array.from(map.entries()).map(([name, days]) => ({name, days}))
})

function getClass(type) {
  const map = {
    Tillganglig: 'available',
    Franvaro: 'absence',
    Fullbokad: 'fullybooked',
    Bokad50: 'booked/50',
    Prifullbokad: 'pri-booked',
    Pribokad50: 'pri-booked50',
  }
  return map[type] || ''
}
</script>

<style scoped>

.booking-grid {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>