<template>
  <div>
    <VWeatherNav :city="currentWeatherObj.city" :country="currentWeatherObj.country"></VWeatherNav>
    <div class="weather-container">
      <div class="data-container">
        <p class="standart-info">{{ currentWeatherObj.weather }}, {{ currentWeatherObj.aboutWeather }}</p>
        <div class="additional-indicators">
          <div class="indicator">
            <p class="standart-info"><img class="icon" src="../assets/icons/iconHumidity.png">{{ currentWeatherObj.humidity }} %</p>
            <p class="standart-info"><img class="icon" src="../assets/icons/iconPressure.png">{{ currentWeatherObj.pressure }} mmhg</p>
          </div>
          <div class="indicator">
            <p class="standart-info"><img class="icon" src="../assets/icons/iconWind.png">{{ currentWeatherObj.windSpeed }} m/s</p>
            <p class="standart-info"><img class="icon" src="../assets/icons/iconVisibility.png">{{ currentWeatherObj.visibility }} km</p>
          </div>
        </div>
      </div>
    </div>
    <div class="date">
      <p class="temperature">{{ currentWeatherObj.temperature }}&deg;</p>
      <p class="feels-like">Feels like {{ currentWeatherObj.feelsLike }}°</p>
    </div>
  </div>
</template>

<script>
  import VWeatherNav from '@/components/VWeatherNav.vue'
  import axios from 'axios'
  export default {
    data() {
      return {
        // nameLocationObj: {},
        weatherInfoObj: {},
        currentWeatherObj: {
          id: null,
          city: null,
          country: null,
          temperature: null,
          feelsLike: null,
          weather: null,
          aboutWeather: null,
          visibility: null,
          humidity: null,
          windSpeed: null,
          pressure: null

        }
      }
    },
    async beforeCreate() {
      this.weatherInfoObj = await axios.get('https://api.openweathermap.org/data/2.5/weather?lat=55.75&lon=37.61&appid=6c9795955fc786f11b8ba06bcf74eb19')
      this.returnCorrectData()
    },

    methods: {
      returnCorrectData() {
        this.currentWeatherObj.city = this.weatherInfoObj.data.name
        this.currentWeatherObj.country = this.weatherInfoObj.data.sys.country
        this.currentWeatherObj.temperature = Math.floor(this.weatherInfoObj.data.main.temp / 273.15)
        this.currentWeatherObj.feelsLike = Math.floor(this.weatherInfoObj.data.main.feels_like / 273.15)
        this.currentWeatherObj.weather = this.weatherInfoObj.data.weather[0].main
        this.currentWeatherObj.aboutWeather = this.weatherInfoObj.data.weather[0].description
        this.currentWeatherObj.visibility = this.weatherInfoObj.data.visibility/1000
        this.currentWeatherObj.humidity = this.weatherInfoObj.data.main.humidity
        this.currentWeatherObj.windSpeed = this.weatherInfoObj.data.wind.speed
        this.currentWeatherObj.pressure = Math.floor(this.weatherInfoObj.data.main.pressure * 0.75)

      }
    },
    computed: {
      checkedWeather() {
        if(this.weatherInfoObj.data) {
          return this.weatherInfoObj.data
        } else {
          return 0
        }
      }
    },
    components: {
      VWeatherNav
    }
  }
</script>