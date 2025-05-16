<template>
  <div class="month-nav">
    <button @click="goBackMonth" class="nav-btn">
      <img src="../assets/icons/back-btn.svg" alt="back-btn">
    </button>
    <div id="display-text">
      <div id="view-months">{{ props.displayMonth }}</div>
      <div id="view-year">{{ props.currentYear }}</div>
    </div>
    <button @click="goForwardMonth">
      <img src="../assets/icons/forward-btn.svg" alt="forward-btn">
    </button>
  </div>
</template>
<script setup>

const props = defineProps({
  displayMonth: String,
  currentYear: Number,
  startDate: Date,
  endDate: Date,
  viewMode: Number  // used to toggle different grids by months.
})

const emit = defineEmits(["go-back-month", "go-forward-month"])

const goBackMonth = () => {
  emit("go-back-month")
}

const goForwardMonth = () => {
  emit("go-forward-month")
}

</script>
<style>

.nav-btn {
  cursor: pointer;
}
.month-nav {
  display: flex;
  width: 235px;
  height: 100px;
  background-color: #F6F6F6;
  justify-content: space-between;
  border-radius: 20px 20px 0 0 ;
  overflow: hidden;
}

#display-text {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-self: center;
}

#view-year {
  align-self: center;
}
#view-months {
  font-weight: bold;
}

button {
  position: relative;
  border: 0;
  background-color: #F6F6F6;

}
</style>