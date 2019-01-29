<template>
  <div id="app">
    <h1>Calendar App</h1>
    <h2>Javascript: HTML/CSS Code Verification Challenge</h2>
    <h4>{{ month }}</h4>
    <b-container>
      <b-row>
        <calendar :month="month"></calendar>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Calendar from './components/calendar/Calendar.vue';

export default {
  components: {
    Calendar
  },
  data() {
    return {
      months: [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'Octuber',
        'November',
        'December'
      ]
    }
  },
  computed: {
    month() {
      return this.months[new Date().getMonth()];
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}

h1 {
  font-weight: normal;
}

h2 {
  font-weight: lighter;
  margin-bottom: 60px;
}
</style>