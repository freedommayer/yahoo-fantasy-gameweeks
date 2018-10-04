<template>
  <div id="app">
    <games-listing :games="games"></games-listing>
  </div>
</template>

<script>
import ScheduleByGameWeeks from './json/schedule-by-game-weeks.json';
import GamesListing from './components/GamesListing.vue';

export default {
  name: 'app',

  components: {
    GamesListing
  },

  data() {
    return {
      games: ScheduleByGameWeeks
    };
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
  }

  #app {
    min-height: 100vh;
    padding: 50px;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
</style>
