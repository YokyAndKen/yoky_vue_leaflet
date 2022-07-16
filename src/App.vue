<template>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/> -->
  <div id="map"></div>
  <!-- <draw-tool></draw-tool> -->
</template>

<script lang='ts'>
// import { defineComponent } from '@vue/composition-api'

import { onMounted, provide } from '@vue/runtime-core'
import L from 'leaflet'
// import DrawTool from './components/drawTool.vue'

export default {
  name: 'App',
  // components: {
  //   DrawTool
  // },
  setup() {
    let map = {}
    let parent = { map };
    provide('map', parent);
    onMounted(() => {
      map = L.map('map', {
        crs: L.CRS.EPSG4326,
        center: [40, 118],
        maxZoom: 18,
        zoom: 6,
      })
      parent.map = map;
      let url = "https://iserver.supermap.io/iserver/services/map-world/rest/maps/World";
      L.supermap.tiledMapLayer(url , {noWrap: true}).addTo(map);
    })

  },
}
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
