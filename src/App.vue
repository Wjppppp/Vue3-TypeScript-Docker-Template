<script lang="ts">
import './assets/main.css'
import { defineComponent } from 'vue'
// leaflet map module
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default defineComponent({
  // type definition
  props: {
    name: String,
    msg: { type: String}, // title
    map: { type: null }, // map container
  },
  data(){
    return {
      msg: 'Leaflet Map',
      map: null,
    }
  },
  mounted(){
    // initiate map
    this.initMap();
  },
  methods: {
    // initiate map
    initMap(){
      let map = this.map
      map = L.map("mapContainer").setView([51.04, 13.72], 10);

      // map layer
      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '© OpenStreetMap'
      }).addTo(map);    

      // map marker
      L.marker([51.04733, 13.730164]).addTo(map).bindPopup("Hello, I am in Dresden");

      // map polygon
      L.polygon([
        [51.03, 13.71],
        [51.03, 13.74],
        [51.06, 13.74],
        [51.06, 13.71]
      ]).addTo(map);

      this.map = map;   
    },
    // add marker button
    addMarker(){
      let map = this.map;
      let mark = function(ev: any) {     
        let marker = L.marker(ev.latlng).addTo(map);       
        marker.bindPopup("Hello, I am at <br>(" + ev.latlng.lat + "," + ev.latlng.lng + ").").openPopup();
      }
      map.once('click', mark);
    },
  
  },
  beforeDestroy() {
    if (this.map) {
      this.map.remove();
    }
  }

})

</script>

<template>
  <main>
    <h1>{{msg}}</h1>
  </main>
  <div id="mapContainer"></div>
  <button @click="addMarker" class="btn">Add Marker</button>
</template>

<style scoped>
  #mapContainer {
    width: 600px;
    height: 400px;
    background-color: white;
  }
  .btn {
    margin: 20px;
  }
</style>
