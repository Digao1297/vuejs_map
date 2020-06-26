<template>
  <div class="vmap">
    <div
      :style="`height:${this.height}px; width:${this.width}px`"
      id="map"
    ></div>
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl";
import sc_json from "../services/santaCatarina.json";
export default {
  name: "vmap",
  props: {
    accessToken: {
      type: String,
      required: true,
    },
    mapStyle: {
      type: String,
      required: true,
    },
    position: {
      type: Array,
    },
    zoom: {
      type: Number,
    },
    width: {
      type: String,
      required: true,
      default: "500",
    },
    height: {
      type: String,
      required: true,
      default: "400",
    },
  },

  methods: {
    createMap() {
      mapboxgl.accessToken = this.accessToken;
      let map = new mapboxgl.Map({
        container: "map",
        zoom: this.zoom,
        attributionControl: false,
        center: this.position,
        style: this.mapStyle,
      });
      map.addControl(new mapboxgl.NavigationControl());
      map.on("load", () => {
        map.addLayer({
          id: "route",
          type: "line",
          source: {
            type: "geojson",
            data: sc_json,
          },
          layout: {
            "line-join": "round",
            "line-cap": "round",
          },
          paint: {
            "line-color": "#ff0000",
            "line-width": 1,
          },
        });
      });
    },
  },
  mounted() {
    this.createMap();
  },
};
</script>
