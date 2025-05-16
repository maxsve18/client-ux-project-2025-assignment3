<template>
  <div class="dropdowns">
    <div class="dropdown-wrapper">
      <div id="availability-dropdown" class="dropdown">
        <button @click="toggleAvailabilityDropdown" id="availability-btn">
          Omfattning
          <img src="../assets/icons/availability.svg" id="availability-icon" alt="availability icon">
          <img src="../assets/icons/chevron.svg" class="chevron-icon" :class="{ 'rotate': showAvailabilityDropdown }"
               alt="chevron icon">
        </button>
        <div v-if="showAvailabilityDropdown" class="availability-dropdown-menu">
          <div class="dropdown-item">Tillgänglig <img src="../assets/status/available.svg" alt="available icon"/></div>
          <div class="dropdown-item">Frånvaro <img src="../assets/status/absence.svg" alt="absence icon"/></div>
          <div class="dropdown-item">Fullbokad <img src="../assets/status/booked100.svg" alt="booked100 icon"/></div>
          <div class="dropdown-item">Bokad 50% <img src="../assets/status/booked50.svg" alt="booked50 icon"/></div>
          <div class="dropdown-item">Prl. Fullbokad <img src="../assets/status/pre100.svg" alt="pre100 icon"/></div>
          <div class="dropdown-item">Prl. Bokad 50% <img src="../assets/status/pre50.svg" alt="pre50 icon"/></div>
        </div>
      </div>

      <div id="jobrole-dropdown" class="dropdown">
        <button @click="toggleJobroleDropdown" id="jobrole-btn">
          Alla hantverkare
          <img src="../assets/icons/chevron.svg" class="chevron-icon" :class="{ 'rotate': showJobroleDropdown }"
               alt="chevron icon">
        </button>
        <div v-if="showJobroleDropdown" class="jobrole-dropdown-menu">
          <div class="dropdown-item-jb">
            <img src="../assets/craftman/carpenter.svg" alt="carpenter icon"/> Snickare
            <input type="checkbox" name="filter" class="job-checkbox">
          </div>
          <div class="dropdown-item-jb">
            <img src="../assets/craftman/plumber.svg" alt="plumber icon"/> Rörmokare
            <input type="checkbox" name="filter" class="job-checkbox">
          </div>
          <div class="dropdown-item-jb">
            <img src="../assets/craftman/electrician.svg" alt="electrician icon"/> Elektriker
            <input type="checkbox" name="filter" class="job-checkbox">
          </div>
          <div class="dropdown-item-jb">
            <img src="../assets/craftman/painter.svg" alt="painter icon"/> Målare
            <input type="checkbox" name="filter" class="job-checkbox">
          </div>
          <div class="dropdown-item-jb">
            <img src="../assets/craftman/mason.svg" alt="mason icon"/> Murare
            <input type="checkbox" name="filter" class="job-checkbox">
          </div>
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

.dropdowns {
  width: 175px;
}

.dropdowns * {
  font-family: 'Inter', sans-serif;
}


#availability-dropdown {
  margin-bottom: 20px;
}

#availability-btn {
  font-size: 17px;
  font-weight: 600;
  color: #333333;
  background-color: #F6F6F6;
  border: 1px solid #9C9C9C;
  border-radius: 5px;
  cursor: pointer;
  display: flex;
  align-items: center;
  text-align: left;
  width: 100%;
  height: 45px;
}

#availability-icon {
  margin: 0 5px 0 25px;
}

.availability-dropdown-menu {
  position: relative;
  padding-left: 5px;
  bottom: 11px;
  height: 200px;
  border: 1px solid #9C9C9C;
  border-top: 0;
  border-radius: 0 0 5px 5px;
  font-size: 13px;
  background-color: #F6F6F6;
  text-align: left;
}


.dropdown-item,
.dropdown-item-jb {
  font-size: 12px;
  display: flex;
  position: relative;
  top: 5px;
  margin-top: 7px;
}

.dropdown-item {
  justify-content: space-between;
  cursor: pointer;
}

.dropdown-item img,
.dropdown-item-jb img {
  margin-bottom: 5px;
  margin-right: 35px;
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
  font-size: 17px;
  color: #333333;
  background-color: #F6F6F6;
}

#jobrole-btn img {
  margin-left: 2px;
}

.jobrole-dropdown-menu {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  position: relative;
  padding-left: 5px;
  bottom: 11px;
  height: 185px;
  width: 173px;
  border: 1px solid #9C9C9C;
  border-top: 0;
  border-radius: 0 0 5px 5px;
  font-size: 13px;
  background-color: #F6F6F6;
}

.jobrole-dropdown-menu img {
  margin-right: 10px;
  width: 20px;
}

.job-checkbox {
  position: absolute;
  cursor: pointer;
  margin: 0;
  left: 105px;
  width: 20px;
  height: 20px;
}

.chevron-icon.rotate {
  transform: rotate(180deg);
}
</style>