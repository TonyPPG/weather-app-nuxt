<!-- Single Weather Card Component -->
<template>
  <transition name="slide" type="animation" appear>
    <div class="card weather-card">
      <transition name="rolling" appear>
        <img
          class="weather-icon"
          :src="
            require(`~/assets/images/weathers/${weather._weatherConditionIcon}.svg`)
          "
        />
      </transition>
      <!-- <div :class="weather._weatherConditionIcon | toHeaderClass "> -->
      <div :class="'card-header' + ' header-' + weather._weatherConditionIcon">
        <h4 class="card-title">
          {{ weather._name }} -- {{ weather._country._name }}
        </h4>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="condition col-md-6 col-sm-6">
            <h5>
              {{ weather._weatherCondition ? weather._weatherCondition : "--" }}
            </h5>
          </div>
          <div class="temperature col-md-6 col-sm-6">
            <h5>{{ weather._weatherTemp ? weather._weatherTemp : "--" }} ℃</h5>
          </div>
        </div>
      </div>
      <ul class="list-group list-group-flush">
        <li class="list-group-item">
          {{ weather._weatherWind }}
          <div class="float-right">
            <img src="~/assets/images/weathers/wind.svg" class="small-icon" />
          </div>
        </li>
        <li class="list-group-item">
          {{ weather._weatherHumidity }}
          <div class="float-right">
            <img
              src="~/assets/images/weathers/humidity.svg"
              class="small-icon"
            />
          </div>
        </li>
        <li class="list-group-item">
          Last Update: {{ weather._weatherLastUpdated | toDateTime }}
        </li>
      </ul>
    </div>
  </transition>
</template>

<script>
import moment from "moment";

export default {
  props: ["weather"],
  data() {
    return {};
  },
  filters: {
    /* Filter to convert epoch to readable datetime */
    toDateTime(value) {
      if (value) {
        return moment.unix(value).format("MMMM Do YYYY, h:mm:ss a");
      }
      return "N/A";
    },
  },
};
</script>

<style lang="scss" src="../../assets/styles/weathers/weather-card.scss" />