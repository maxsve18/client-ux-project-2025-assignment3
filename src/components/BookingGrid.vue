<template>
  <div class="booking-grid">
    <!-- background -->
      <img class="background-grid" src="../assets/grid/background-grid.svg" alt="bg-grid">

    <!-- overlay -->
    <!--Fix this so when you click on Month Navigator the layout changes to sqquare grid 2 -->
    <div v-if="viewMode === 1" class="square-grid-1">
      <img src="../assets/grid/row1.svg" alt="row-1">
      <img src="../assets/grid/row2.svg" alt="row-2">
      <img src="../assets/grid/row3.svg" alt="row-3">
      <img src="../assets/grid/row4.svg" alt="row-4">
    </div>
    <div v-else class="square-grid-2">
      <img src="../assets/grid/row5.svg" alt="row-1">
      <img src="../assets/grid/row6.svg" alt="row-2">
      <img src="../assets/grid/row7.svg" alt="row-3">
      <img src="../assets/grid/row8.svg" alt="row-4">

    </div>
  </div>
</template>
<script setup lang="js">

const props = defineProps({
  viewMode: Number
})

</script>

<style scoped>


.booking-grid {
  position: relative;
  width: fit-content;
  display: inline-block;
}
.background-grid {
  display: block;
  width: 100%;
  height: auto;
}
.square-grid-1 {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  flex-direction: row;
  margin-left: 35px;
  margin-top: 45px;
  gap: 70px;
}

.square-grid-2 {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  flex-direction: row;
  margin-left: 35px;
  margin-top: 45px;
  gap: 70px;
}

.square-grid-1 img,
.square-grid-2 img {
  width:100%;
  height: auto;
}
</style>