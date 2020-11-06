<!--
    Header Component
-->
<template>
  <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
    <div class="container-fluid">
      <!-- Brand and toggle get grouped for better mobile display -->
      <div class="navbar-header">
        <NuxtLink to="/" class="navbar-brand">Weather APP</NuxtLink>
      </div>
      <!-- /.navbar-collapse -->
    </div>
    <!-- /.container-fluid -->
  </nav>
</template>

<script>
import { mapActions } from "vuex";

export default {
  methods: {
    ...mapActions({
      fetchWeathers: "loadWeathers",
    }),
    loadWeathers() {
      //   this.fetchWeathers();
      console.log("load weather here");
    },
  },
  created() {
    this.loadWeathers();
  },
};
</script>