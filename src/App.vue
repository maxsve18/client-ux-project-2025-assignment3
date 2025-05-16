<template>
  <div class="app-wrapper">
    <div class="container">
      <div class="sidebar">
        <div id="top">
          <div class="profile">
            <img src="./assets/icons/anna.svg" alt="Anna avatar">
            <div class="profile-info">
              <p>Anna Karlsson</p>
              <p>Svenssons Hantverk AB</p>
            </div>
          </div>

          <nav>
            <ul class="nav-links">
              <li><a href="#" class="active">Bokningsschema</a></li>
              <li><a href="#">Statistik</a></li>
              <li><a href="#">Inställningar</a></li>
              <li><a href="#">Logga ut</a></li>
            </ul>
          </nav>
        </div>
        <div id="header">
          <h1>Bokningsschema</h1>
          <div id="month-navigator">
            <MonthNavigator
                :displayMonth="displayMonth"
                :current-year="currentYear"
                :startDate="startDate"
                :endDate="endDate"
                :viewMode="viewMode"
                @go-back-month="goBackMonth"
                @go-forward-month="goForwardMonth"
            />
          </div>
        </div>
      </div>
      <main>
        <div class="filter">
          <Dropdowns/>
          <WorkerList/>
        </div>
        <div id="month-grid">
          <WeekView :startDate="startDate" :endDate="endDate"/>
          <BookingGrid :viewMode="viewMode"/>
        </div>
      </main>
    </div>
  </div>
</template>

<style>
.app-wrapper {
  display: flex;
  justify-content: center; /* horisontell centrering */
  align-items: center;
  min-width: 1600px;
}

.container {
  width: 1440px;
  background-color: #F6F6F6;
}

#top {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-top: 20px;
}

.sidebar {
  display: flex;
  flex-direction: column;
  background-color: #E3DCD2;
  width: 100%;
  height: 240px;
  margin-bottom: 20px;
}

.profile {
  display: flex;
  flex-direction: row;
  margin-left: 65px;
}

.profile-info {
  font-size: 14px;

  p:first-child {
    font-size: 17px;
    font-weight: bold;
    margin: 40px 0 -20px 0;
  }
}

.nav-links {
  display: flex;
  flex-direction: row;
  margin-right: 65px;

  li {
    list-style-type: none;
    margin-right: 15px;
    margin-left: auto;

    a {
      font-weight: 600;
      color: black;
      text-decoration: none;
    }
  }
}

.active {
  border-bottom: 1px solid black;
}

#header {
  margin-top: 35px;
  margin-left: 70px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  h1 {
    font-size: 40px;
  }
}

#month-navigator {
  position: relative;
  right: 70px;
  button {
    cursor: pointer;
  }
}

filter {
  display: flex;
  flex-direction: column;
  margin-right: 5px;
}

#month-grid {
  padding-right: 100px;
  font-weight: 600;
}

main {
  margin-left: 70px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>

<script>
import Dropdowns from './components/Dropdowns.vue';
import BookingGrid from "./components/BookingGrid.vue";
import WeekView from "./components/WeekView.vue";
import WorkerList from "./components/WorkerList.vue";
import MonthNavigator from "./components/MonthNavigator.vue";

export default {
  name: 'App',
  components: {
    Dropdowns,
    BookingGrid,
    WeekView: WeekView,
    WorkerList,
    MonthNavigator
  },
  data() {
    return {
      viewMode: 1,
      currentYear: 2025,

    };
  },
  computed: {

    startDate() {
      const periods = [
        {start: new Date(this.currentYear, 2, 25)},
        {start: new Date(this.currentYear, 3, 28)},
        {start: new Date(this.currentYear, 4, 26)}
      ]
      return periods[this.viewMode].start
    },
    endDate() {
      const periods = [
        {end: new Date(this.currentYear, 3, 19)},
        {end: new Date(this.currentYear, 4, 23)},
        {end: new Date(this.currentYear, 5, 20)}
      ]
      return periods[this.viewMode].end
    },
    displayMonth() {
      const months = ["Januari", "Februari", "Mars", "April", "Maj", "Juni",
        "Juli", "Augusti", "September", "October", "November", "December"];
      const startMonth = this.startDate.getMonth();
      const endMonth = this.endDate.getMonth()
      return `${months[startMonth]} - ${months[endMonth]}`;
    }
  },
  methods: {
    goBackMonth() {
      if (this.viewMode === 0) {
        this.viewMode = 2;
        this.currentYear--;
      } else {
        this.viewMode--;
      }
    },
    goForwardMonth() {
      if (this.viewMode === 2) {
        this.viewMode = 0
        this.currentYear++
      } else {
        this.viewMode++
      }
    }
  }
}
</script>