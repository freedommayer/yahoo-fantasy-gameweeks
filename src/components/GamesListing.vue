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
      <div v-for="team in orderedTeams" class="games-listing__team">
        ({{ team.length }})

        <img
          v-for="game in team"
          :src="game.logo"
          :alt="game.city"
          class="games-listing__team-logo"/>
      </div>
    </div>
  </div>
</template>

<script>
import { groupBy, sortBy } from 'underscore';

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
      this.orderedTeams = this.formatGameWeek(this.schedule.gameWeeks[index]);
    }
  },

  mounted() {
    this.orderedTeams = this.formatGameWeek(this.schedule.gameWeeks[0]);
  },

  methods: {
    formatGameWeek(gameWeek) {
      let allTeams = [],
          groupedTeams = [];

      for (let day in gameWeek) {
        let teams = gameWeek[day];

        for (let team in teams) {
          allTeams.push(teams[team]);
        }
      }

      groupedTeams = groupBy(allTeams, 'city');

      return sortBy(groupedTeams, 'length').reverse();
    }
  }
}
</script>

<style scoped>
  .games-listing__filters {
    margin-bottom: 25px;
  }

  .games-listing__week {
    display: flex;
    flex-direction: column;
  }

  .games-listing__day {
    margin-bottom: 20px;
  }

  .games-listing__label {
    font-weight: 700;
  }

  .games-listing__team {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    margin-bottom: 10px;

    &:last-child {
      margin-bottom: 0;
    }
  }

  .games-listing__team-logo {
    width: 40px;
    margin: 0 5px;
  }
</style>
