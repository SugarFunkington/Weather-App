<template>
  <div id="app" :style="{'background-image': bg_url}">
    <main>
      <SearchBar @search="fetchWeather"/>
      <div class="display" v-if="!this.loading">
        <LocationDisplay :location="this.location" />
        <WeatherDisplay :weather="this.weather" />
      </div>
      <div class="loading" v-if="this.loading">
        <LoadingSpinner />
      </div>

    </main>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue'
import LocationDisplay from './components/LocationDisplay.vue'
import WeatherDisplay from './components/WeatherDisplay.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'

export default {
  name: 'App',
  components: {
    SearchBar,
    LocationDisplay,
    WeatherDisplay,
    LoadingSpinner
  },
  data () {
    return {
      loading:true,
      // Weather API Data
      api_key: '0a0ae273264b3a2facc2da4dc3b568f6',
      weather_url: 'https://api.openweathermap.org/data/2.5/weather?',
      geo_url:'https://api.openweathermap.org/geo/1.0/direct?q=',
      weather: {},
      location: {},
      // Unsplash API Data
      unsplash_access_key: 'uDBYoGP7lAboj7OD6BwdHS-aOHeN25wlsdru5oAbwOE',
      unsplash_secret_key: 'lmNiBcvmGymi4UTPTDSrUCAYrGGlAzNx_cUduOwheNQ',
      bg_url: ""
    }
  },
  methods: {
    async fetchWeather(query) {
      // Enable page loading state
      this.loading = true

      let latitude = ""
      let longitude = ""

      // check if using Lat/Lon Object or Location String
      if (typeof query === "string") {
        // Fetch lat/lon using location string
        const res = await fetch(`${this.geo_url}${query}&limit=1&appid=${this.api_key}`)
        const latLon = await res.json()
        latitude = latLon[0].lat
        longitude = latLon[0].lon
      } else {
        // Set lat/lon using user location
        latitude = query.coords.latitude
        longitude = query.coords.longitude
      }

      // Fetch the Weather for Lat/Lon
      const weatherRes = await fetch(`${this.weather_url}lat=${latitude}&lon=${longitude}&units=metric&appid=${this.api_key}`)
      const weather = await weatherRes.json()

      // Set weather
      this.weather = weather
      
      // Set location
      const countryCode = this.weather.sys.country
      const country = new Intl.DisplayNames(['en'], {type:'region'}).of(countryCode)

      this.location = {
        locality: this.weather.name,
        country: country
      }

      // Set new background image using weather description
      this.getBgPhoto(this.weather.weather[0].description)

      // Disable the loading state
      this.loading = false
    },
    async getBgPhoto (weatherDescription) {
      // Define Unsplash search queries
      let urlQuery = weatherDescription.replace(' ', '+').concat('+weather')

      // Search for a new bg image
      const res = await fetch(`https://api.unsplash.com/photos/random/?client_id=${this.unsplash_access_key}&query=${urlQuery}`)
      const data = await res.json()

      // Set new background URL
      this.bg_url = `url(${data.links.download})`
    }
  },
  async created() {
    // Get user location on load
    navigator.geolocation.getCurrentPosition(position => this.fetchWeather(position));
  }
  
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;900&display=swap');
* {
  margin:0;
  padding:0;
  box-sizing:border-box;
}

html, body {
  font-family:'Poppins', sans-serif !important;
}

#app {
  background-image:url('./assets/bg.webp');
  background-size:cover;
  background-position:bottom;
  transition:0.4s;
}

main {
  min-height:100vh;
  padding:25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
}

</style>
