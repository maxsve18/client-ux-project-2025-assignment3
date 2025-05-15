<template>
  <div class="dropdowns">
    <div class="dropdown-wrapper">
      <div id="availability-dropdown" class="dropdown">
        <button @click="toggleAvailabilityDropdown" id="availability-btn">Omfattning
          <img src="../assets/availability.svg" id="availability-icon">
          <img src="../assets/chevron.svg" class="chevron-icon" :class="{ 'rotate': showAvailabilityDropdown }"></button>
        <div v-if="showAvailabilityDropdown" class="availability-dropdown-menu">
          <div class="dropdown-item">
            Tillgänglig
            <img src="../assets/status/available.svg"/>
          </div>
          <div class="dropdown-item">Frånvaro
            <img src="../assets/status/absence.svg"/></div>
          <div class="dropdown-item">Fullbokad
            <img src="../assets/status/booked100.svg"/></div>
          <div class="dropdown-item">Bokad 50%
            <img src="../assets/status/booked50.svg"/></div>
          <div class="dropdown-item">Prl. Fullbokad
            <img src="../assets/status/pre100.svg"/></div>
          <div class="dropdown-item">Prl. Bokad 50%
            <img src="../assets/status/pre50.svg"/></div>
        </div>
      </div>

      <div id="jobrole-dropdown" class="dropdown">
        <button @click="toggleJobroleDropdown" id="jobrole-btn">Alla hantverkare
          <img src="../assets/chevron.svg" class="chevron-icon" :class="{ 'rotate': showJobroleDropdown }"></button>
        <div v-if="showJobroleDropdown" class="jobrole-dropdown-menu">
          <div class="dropdown-item">Snickare</div>
          <div class="dropdown-item">Rörmokare</div>
          <div class="dropdown-item">Elektriker</div>
          <div class="dropdown-item">Målare</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue';

const showAvailabilityDropdown = ref(false);
const showJobroleDropdown = ref(false);

function toggleAvailabilityDropdown() {
  showAvailabilityDropdown.value = !showAvailabilityDropdown.value;
}

function toggleJobroleDropdown() {
  showJobroleDropdown.value = !showJobroleDropdown.value;
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

#availability-dropdown {
  margin-bottom: 20px;
}

.dropdowns {
  width: 160px;
  * {
    font-family: 'Inter', sans-serif;
  }
}

#availability-btn {
  font-size: 13px;
  color: #333333;
  padding-left: 5px;
  display: flex;
  align-items: center;
  text-align: left;
  border: 1px solid #9C9C9C;
  border-radius: 5px;
  cursor: pointer;
  width: 100%;
  height: 45px;
  font-weight: 600;
  background-color: #E2E2E2;
}

#availability-icon {
  margin-right: 6px;
  margin-left: 26px;
}

.availability-dropdown-menu {
  position: relative;
  padding-left: 5px;
  bottom: 11px;
  height: 200px;
  border: 1px solid #9C9C9C;
  border-top: 0;
  border-radius: 0 0 5px 5px;
  text-align: left;
  font-size: 13px;
  font-weight: lighter;
  background-color: #E2E2E2;
}

.jobrole-dropdown-menu {
  position: relative;
  bottom: 11px;
  height: 120px;
  border: 1px solid #9C9C9C;
  border-top: 0;
  border-radius: 0 0 5px 5px;
  text-align: left;
  font-size: 13px;
  font-weight: lighter;
  background-color: #E2E2E2;
}

#jobrole-btn {
  display: flex;
  align-items: center;
  text-align: left;
  border: 1px solid #9C9C9C;
  border-radius: 5px;
  cursor: pointer;
  width: 100%;
  height: 44px;
  font-weight: 600;
  color: #333333;
  background-color: #E2E2E2;
}

.dropdown-item {
  font-size: 12px;
  display: flex;
  position: relative;
  justify-content: space-between;
  top: 5px;
  cursor: pointer;
  margin-top: 7px;
  img {
    margin-bottom: 5px;
    margin-right: 35px;
  }
}

.chevron-icon.rotate {
  transform: rotate(180deg);
}
</style>