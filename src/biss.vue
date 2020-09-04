<template>
  <div id="app">
    <h1>TEST MapBox</h1>
    <div id="map"></div>
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  name: "App",
  mounted() {
    mapboxgl.accessToken =
      "pk.eyJ1Ijoia2JlbGxpb3VtIiwiYSI6ImNrZTRhcmF4cDAzaGszMW8wNDV2Z2QzZzcifQ.J5LPD_0NDU974meLRh5qBw";
    new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [-74.5, 40],
      zoom: 6
    });
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#map {
  height: 100vh;
}
</style>
