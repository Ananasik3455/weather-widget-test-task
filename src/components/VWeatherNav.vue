<template>
  <div class="weatherIcon">
    <div class="icon-container">
      <img class="icon" src="../assets/icons/iconSun.png">
    </div>
    <div class="location-container">
      <p
        v-if="this.$route.path == '/'"
        class="city"
      >
        {{ city }}, {{ country }}
      </p>
      <div
        v-else
        class="button-container"
      >
        <input
          class="search"
          type="text"
          name="search"
          placeholder="City"
          v-model="nameCity"
        >
        <button
          class="button-settings"
          @click="getCoordCity"
        >
          <img
            class="icon-search"
            src="../assets/icons/iconArrow.png"
          >
        </button>
      </div>


    </div>
    <div class="button-container">
      <button class="button-settings" @click="changeLink">
        <img class="icon" src="../assets/icons/settings.png" alt="">
      </button>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data() {
      return {
        nameCity: '',
        allInfoCityObj: {},
        coordCityObj: {
          lat: '',
          lon: ''
        }
      }
    },
    methods: {
      changeLink () {
        const linkPage = this.$route.path
        if (linkPage == '/') {
          this.$router.push('/viewSettings')
        } else this.$router.push('/')
      },
      async getCoordCity () {
        const changeCity = this.nameCity
        console.log(changeCity)
        this.allInfoCityObj = await axios.get(`http://api.openweathermap.org/geo/1.0/direct?q=${ changeCity }&limit=1&appid=6c9795955fc786f11b8ba06bcf74eb19`)
        this.coordCityObj.lat = this.allInfoCityObj.data[0].lat
        this.coordCityObj.lon = this.allInfoCityObj.data[0].lon
        console.log(this.coordCityObj)
      }
    },
    props: ['city', 'country']
  }
</script>