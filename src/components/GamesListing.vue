<template>
  <div class="games-listing">
    <div class="games-listing__filters">
      <select v-model="currentWeekIndex">
        <option
          v-for="(gameWeek, index) in games.gameWeeks"
          v-text="'Game week ' + (index + 1)"
          :value="index">
        </option>
      </select>
    </div>

    <div v-for="(gameWeek, index) in games.gameWeeks" v-if="currentWeekIndex === index" class="games-listing__week">
      <div v-for="(day, date) in gameWeek" class="games-listing__day">
        <div class="games-listing__label">
          {{ date }}
        </div>

        <div class="games-listing__teams">
          <div v-for="team in day" class="games-listing__team">
            <img class="games-listing__logo" :src="team.logo" :alt="team.city"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GamesListing',

  props: {
    games: { type: Object, required: true }
  },

  data() {
    return {
      currentWeekIndex: 0,
      gameWeek: {}
    };
  },

  mounted() {
    this.test();
  },

  methods: {
    test() {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
