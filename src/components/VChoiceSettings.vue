<template>
  <VWeatherNav></VWeatherNav>
  <div class="weather-container">
    <div class="city-container">
      <img src="../assets/icons/iconHamburger.png" alt="" class="icon-city">
      <p class="city-name">{{ }}</p>
      <button class="button-delete">
        <img src="../assets/icons/iconRecyclingBin.png" alt="" class="icon-delete">
      </button>
    </div>
  </div>
</template>

<script>
import VWeatherNav from '@/components/VWeatherNav.vue'

export default {
  data() {
    return {
      nameCity: ''
    }
  },
  components: {
    VWeatherNav
  }
}
</script>