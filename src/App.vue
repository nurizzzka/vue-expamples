<template>
  <div id="app">
    <SearchBox />
    <WeatherView />
  </div>
</template>

<script>
import WeatherView from './components/WeatherView.vue'
import SearchBox from "./components/SearchBox";

export default {
  name: 'App',
  components: {
    SearchBox,
    WeatherView,
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Roboto', sans-serif;
  }

  #app {
    background: linear-gradient(to bottom, #847f9c, #d1e8ff);
    -webkit-background-size: cover;
    background-size: cover;
    width: 100%;
    height: 100vh;
    padding: 2rem 1rem;
  }
</style>
