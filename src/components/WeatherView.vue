<template>
  <div>
    <div class="weather-box" v-if="typeof weather.main != 'undefined'">
      <div class="city">
        <h3 class="city-name">
          {{ weather.name }}, {{ weather.sys.country }}
        </h3>
        <p class="date">
          {{ getDate() }}
        </p>
      </div>
      <div class="weather-info">
        <h2 class="temperature">{{ Math.round(weather.main.temp) }}°C</h2>
        <p class="weather-type">{{ weather.weather[0].main }}</p>
      </div>
    </div>

    <div v-else>
      <h2>Enter the name of city</h2>
    </div>
  </div>

</template>

<script>
  import { bus } from "../main";

  export default {

  name: 'WeatherView',
  data() {
    return {
      API_KEY: '7bc15215cad4705cd317d8fc53921dfb',
      API_BASE: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  created() {
    bus.$on('searchCity', data => {
      this.query = data
      fetch(`${this.API_BASE}weather?q=${this.query}&units=metric&APPID=${this.API_KEY}`)
              .then(response => response.json())
              .then(this.setState)
    })
  },
  methods: {
    setState (results) {
      this.weather = results
    },
    getDate() {
      let date = new Date()
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
      let weekdays = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]

      let d = date.getDate()
      let day = weekdays[date.getDay()]
      let month = months[date.getMonth()]
      let year = date.getFullYear()

      return `${day} ${d} ${month} ${year}`

    }
  },
  }
</script>

<style scoped>
  .weather-box {
    background: rgba(255,255,255,0.3);
    border-radius: 20px;
    padding: 2rem 0;
    box-shadow: 2px 3px 10px rgba(0,0,0,0.3);
  }

  div > * {
    color: white;
    text-align: center;
  }

  .city .city-name {
    font-size: 3rem;
    text-shadow: 2px 3px rgba(0,0,0,0.3);
  }

  .city .date {
    font-weight: 200;
    font-size: 1.3rem;
  }

  .weather-info .temperature {
    margin: 25px;
    font-size: 6rem;
    text-shadow: 3px 5px 2px rgba(0,0,0,0.3);
    font-style: italic;
  }

  .weather-info .weather-type {
    font-size: 2.4rem;
    text-shadow: 3px 3px 2px rgba(0,0,0,0.3);

  }
</style>
