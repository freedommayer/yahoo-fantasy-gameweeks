<template>
  <div class="games-listing">
    <div class="games-listing__filters">
      <select v-model="currentWeekIndex">
        <option
          v-for="(gameWeek, index) in schedule.gameWeeks"
          v-text="'Game week ' + (index + 1)"
          :value="index">
        </option>
      </select>
    </div>

    <div class="games-listing__week">
      <img v-for="team in orderedTeams" class="games-listing__logo" :src="team.logo" :alt="team.city"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GamesListing',

  props: {
    schedule: { type: Object, required: true }
  },

  data() {
    return {
      currentWeekIndex: 0,
      orderedTeams: {}
    };
  },

  watch: {
    currentWeekIndex(index) {
      let currentGameWeek = this.schedule.gameWeeks[index];
      this.orderedTeams = this.formatGameWeek(currentGameWeek);
    }
  },

  mounted() {
    this.orderedTeams = this.formatGameWeek(this.schedule.gameWeeks[0]);
  },

  methods: {
    formatGameWeek(gameWeek) {
      let orderedTeams = [];

      for (let day in gameWeek) {
        let teams = gameWeek[day];

        for (let team in teams) {
          orderedTeams.push(teams[team]);
        }
      }

      return orderedTeams.sort(this.compareByCityName);
    },

    compareByCityName(a,b) {
      if (a.city < b.city)
        return -1;
      if (a.city > b.city)
        return 1;
      return 0;
    }
  }
}
</script>

<style scoped>
  .games-listing {
    max-width: 800px;
    margin: 0 auto;
  }

  .games-listing__week {
    border: 10px solid green;
  }

  .games-listing__day {
    margin-bottom: 20px;
  }

  .games-listing__label {
    font-weight: 700;
  }

  .games-listing__teams {
    display: flex;
    flex-wrap: wrap;
  }

  .games-listing__logo {
    width: 40px;
  }
</style>
