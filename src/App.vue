<template>
  <div style="overflow-x: auto;">
    <MonthView :startDate="startDate" :endDate="endDate" />
    <AvailabilityDropdown />
  </div>
</template>

<script>
import AvailabilityDropdown from './components/AvailabilityDropdown.vue';
import BookingGrid from "./components/BookingGrid.vue";
import MonthView from "./components/MonthView.vue";

export default {
  name: 'App',
  components: {
    AvailabilityDropdown,
    BookingGrid,
    MonthView
  },
  data() {
    return {
      startDate: new Date(2025, 3, 1), // April 1, 2025
      endDate: new Date(2025, 4, 31)   // May 31, 2025
    };
  }
};
</script>