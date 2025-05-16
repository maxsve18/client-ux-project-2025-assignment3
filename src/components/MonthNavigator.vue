<template>
    <div>
      <!--navigation butttons -->
      <div class="month-nav">
      <button @click="goBackMonth">
      <img src="../assets/icons/back-btn.svg" alt="back-btn">
      </button>
      <p id="view-months">{{ displayMonth }}</p>
      <p id="view-year">{{ currentyear }}</p>
      <button @click="goForwardMonth">
      <img src="../assets/icons/forward-btn.svg" alt="forward-btn">
      </button>
      </div>
    </div>
</template>
<script setup lang="js">

const props = defineProps({
  displayMonth: String,
  currentYear: Number,
  startDate: Date,
  endDate: Date,
  viewMode: Number
})

const emit = defineEmits(["go-back-month", "go-forward-month"])

const goBackMonth = () => {
  emit("go-back-month")
}

const goForwardMonth = () => {
  emit("go-forward-month")
}

</script>