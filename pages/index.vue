<template>
  <div class="container main">
    <app-header></app-header>
    <div class="row">
      <div class="col-md-12">
        <!-- <router-view></router-view> -->
        <app-weather-cards />
      </div>
    </div>
  </div>
</template>

<script>
import Header from '../components/Header.vue';
import WeatherCards from '../components/weathers/WeatherCards';
export default {
  components: {
    appHeader: Header,
    appWeatherCards: WeatherCards
  },
  created() {
    // this.$store.dispatch('initWeathers')
  }
}
</script>

<style lang="scss" src="../assets/styles/home.scss" />
