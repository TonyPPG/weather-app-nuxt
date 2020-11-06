<!--
Weather Card List Component
-->
<template>
  <div>
    <div class="order-group">
      <div class="btn-group" role="group">
        <button
          type="button"
          class="btn btn-secondary"
          @click="orderByAlphabet"
        >
          A-Z
        </button>
        <button
          type="button"
          class="btn btn-secondary"
          @click="orderByTemperature"
        >
          Temperature
        </button>
        <button
          type="button"
          class="btn btn-secondary"
          @click="orderByLastUpdate"
        >
          Last Update
        </button>
      </div>
    </div>
    <div class="search-bar">
      <input
        type="text"
        v-model="search"
        class="form-control"
        placeholder="Filter by Suburb Name / Country Name or Weather Condition"
      />
    </div>
    <!--
      Icons made by <a href="https://www.flaticon.com/authors/iconixar" title="iconixar">iconixar</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> -->
    <div class="row weather-group">
      <div class="col-sm-12 col-md-6"
        v-for="card in filteredWeatherCards"
        v-bind:key="card._venueID">
          <app-weather-card :weather="card"></app-weather-card>
      </div>
    </div>
  </div>
</template>

<script>
import WeatherCard from "./WeatherCard.vue";
//import data for test purpose;
import weathers from "../../data/weathers.js";

export default {
  data() {
    return {
      search: "",
      cards: [],
    };
  },
  components: {
    appWeatherCard: WeatherCard,
  },
  methods: {
    orderByAlphabet() {
      this.cards.sort(function (a, b) {
        if (a._name < b._name) {
          return -1;
        }
        if (a._name > b._name) {
          return 1;
        }
        return 0;
      });
    },
    orderByTemperature() {
      this.cards.sort(function (a, b) {
        if (a._weatherTemp == b._weatherTemp) {
          return 0;
        }
        if (!b._weatherTemp || a._weatherTemp > b._weatherTemp) {
          return -1;
        }
        if (!a._weatherTemp || a._weatherTemp < b._weatherTemp) {
          return 1;
        }
        return 0;
      });
    },
    orderByLastUpdate() {
      this.cards.sort(function (a, b) {
        if (a._weatherLastUpdated > b._weatherLastUpdated) {
          return -1;
        }
        if (a._weatherLastUpdated < b._weatherLastUpdated) {
          return 1;
        }
        return 0;
      });
    },
  },
  computed: {
    /** Filter Weather by Country Name or Weather Condition */
    filteredWeatherCards() {
      return this.cards.filter((element) => {
        return (
          element._name.toLowerCase().match(this.search.toLowerCase()) ||
          (element._weatherCondition &&
            element._weatherCondition
              .toLowerCase()
              .match(this.search.toLowerCase())) ||
          element._country._name.toLowerCase().match(this.search.toLowerCase())
        );
      });
    },
  },
  created() {
    // this.cards = this.$store.getters.weathers;
    this.cards = weathers;
  },
};
</script>

<style lang="scss" src="../../assets/styles/weathers/weather-cards.scss" />