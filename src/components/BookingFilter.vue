<template>
  <div class="dropdowns">
    <div id="availability">
      <label for="availability">Omfattning</label>
        <img :src="Availability" alt="Available icon" id="availability-icon">
        <img :src="Chevron" alt="Chevron icon">
      <select id="availability" name="availability" hidden>
        <option value="available">Tillgänglig</option>
        <option value="absence">Frånvaro</option>
        <option value="booked100">Fullbokad</option>
        <option value="booked50">Bokad 50%</option>
        <option value="pre100">Prl. Fullbokad</option>
        <option value="pre50">Prl. Bokad 50%</option>
      </select>
    </div>

    <div id="job-role">
      <label for="job-role">Alla hantverkare</label>
      <img :src="Chevron" alt="Chevron icon">
      <select id="job-role" name="job-role" hidden>
        <option value="carpenter">Carpenter</option>
        <option value="plumber">Plumber</option>
        <option value="mason">Mason</option>
        <option value="electrician">Electrician</option>
        <option value="painter">Painter</option>
      </select>
    </div>
  </div>
</template>

<script>
import Availability from '../assets/availability.svg';
import Chevron from '../assets/chevron.svg';
import Available from '../assets/status/available.svg';
import Booked50 from '../assets/status/booked50.svg';
import Booked100 from '../assets/status/booked100.svg';
import Pre50 from '../assets/status/pre50.svg';
import Pre100 from '../assets/status/pre100.svg';
import Absence from '../assets/status/absence.svg';

export default {
  data() {
    return {
      Availability,
      Chevron,
      Available,
      Booked50,
      Booked100,
      Pre50,
      Pre100,
      Absence
    };
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap');

body {
  font-family: 'Inter', sans-serif;
  font-size: 17px;
  box-sizing: border-box;
}

.dropdowns {

  div {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 176px;
    height: 44px;
    border: 1px solid black;
    border-radius: 6px;
  }
}

#availability {
  margin-bottom: 30px;
}

#availability-icon {
  margin-left: 16px;
  margin-right: 8px;
}

#job-role {
  label {
    margin-right: 5px;
  }
}
</style>