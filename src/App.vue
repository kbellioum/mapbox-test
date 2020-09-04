<template>
  <div>
    <br />
    <br />
    <div id="geocoder" class="geocoder"></div>
    <br />
    <br />
    <div id="map"></div>
  </div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
import MapboxGeocoder from '@mapbox/mapbox-gl-geocoder'
import '@mapbox/mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css'

export default {
  name: 'mapbox',
  data() {
    return {
      searchString: '',
    }
  },
  mounted() {
    mapboxgl.accessToken =
      'pk.eyJ1Ijoia2JlbGxpb3VtIiwiYSI6ImNrZTRhcmF4cDAzaGszMW8wNDV2Z2QzZzcifQ.J5LPD_0NDU974meLRh5qBw'
    let map = new mapboxgl.Map({
      container: 'map',
      style: 'mapbox://styles/mapbox/streets-v11',
      center: [-74.5, 40],
      zoom: 6,
    })
    map.addControl(new mapboxgl.NavigationControl(), 'top-right')
    map.addControl(new mapboxgl.GeolocateControl(), 'top-right')

    var geocoder = new MapboxGeocoder({
      accessToken: mapboxgl.accessToken,
      mapboxgl: mapboxgl,
    })
    geocoder.addTo('#geocoder')
    geocoder.setRenderFunction((value) => {
      return value.text
    })
    geocoder.on('result', (response) => {
      const options = {
        center: response.result.center,
        zoom: 14,
        essential: true,
      }
      map.flyTo(options)
    })
  },
}
</script>

<style scoped>
#map {
  height: 90vh;
}
.geocoder {
  position: absolute;
  /* z-index: 1; */
  width: 50%;
  left: 50%;
  margin-left: -25%;
  top: 15px;
}
.mapboxgl-ctrl-geocoder {
  min-width: 90%;
}
</style>
