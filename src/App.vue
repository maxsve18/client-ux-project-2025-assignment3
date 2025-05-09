<template>
  <div style="overflow-x: auto;">
    <BookingGrid :bookings="bookingData"/>
  </div>
</template>

<script>
import BookingFilter from './components/BookingFilter.vue';
import BookingGrid from "./components/BookingGrid.vue";
import { bookingData } from "./data/bookingData";

export default {
  components: {
    BookingGrid,
  },
  data() {
    return {
      bookingData: bookingData,
    }
  }
};
</script>