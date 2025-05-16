<template>
  <div style="overflow-x: auto;">
    <div class="test">
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
          </div>
        </div>
        <main>
          <div>
            <MonthNavigator
                :month="currentMonth"
                :year="currentYear"
                :displayMonth="displayMonth"
                :currentyear="currentYear"
                :startDate="startDate"
                :endDate="endDate"
                :viewMode="viewMode"
                @go-back-month="goBackMonth"
                @go-forward-month="goForwardMonth"
            />

            <MonthView :startDate="startDate" :endDate="endDate"/>
            <BookingGrid :viewMode="viewMode"/>
            <Dropdowns/>
          </div>
        </main>
      </div>
    </div>
  </div>
</template>

<style>
.test {
  display: flex;
  justify-content: center; /* horisontell centrering */
  align-items: center;
}

.container {
  max-width: 1440px;
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
  margin-right: 20px;

  li {
    list-style-type: none;
    margin-right: 15px;
    margin-left: auto;

    a {
      color: black;
      text-decoration: none;
    }
  }
}

.active {
  border-bottom: 1px solid black;
}

#header {
  margin-top: 40px;
  margin-left: 70px;
}

main {
  margin-left: 70px;
}
</style>

<script>
import Dropdowns from './components/Dropdowns.vue';
import BookingGrid from "./components/BookingGrid.vue";
import MonthView from "./components/MonthView.vue";
import WorkerList from "./components/WorkerList.vue";
import MonthNavigator from "./components/MonthNavigator.vue";

export default {
  name: 'App',
  components: {
    Dropdowns,
    BookingGrid,
    MonthView,
    WorkerList,
    MonthNavigator
  },
  data() {
    return {
      currentMonth: 3,
      currentYear: 2025,
      viewMode: 1 // to toggle square grid layout
    };
  },
  computed: {
    startDate() {
      return new Date(this.currentYear, this.currentMonth, 28);
    },
    endDate() {
      return new Date(this.currentYear, this.currentMonth + 1, 23);
    },
    displayMonth() {
      const months = ["Januari", "Februari", "Mars", "Aprill", "Maj", "Juni",
        "Juli", "Augusti", "September", "October", "November", "December"];
      return `${months[this.currentMonth]} - ${months[(this.currentMonth + 1) % 12]}`;
    }
  },
  methods: {
    goBackMonth() {
      if (this.currentMonth === 0) {
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
      this.viewMode = this.viewMode === 1 ? 2 : 1; //toggle layout
    },
    goForwardMonth() {
      if (this.currentMonth === 11) {
        this.currentMonth = 0
        this.currentYear++
      } else {
        this.currentMonth++
      }
      this.toggleViewMode()
    },
    toggleViewMode() {
      this.viewMode = this.viewMode === 1 ? 2 : 1
    }
  }
}
</script>