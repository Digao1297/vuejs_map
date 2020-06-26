<template>
  <div class="home">
    <v-row align="center" justify="center">
      <h1>Mapa</h1>
    </v-row>

    <v-row align="center" justify="center">
      <vmap
        :accessToken="token"
        :mapStyle="mapStyle"
        :zoom="5"
        :position="[-51.01303, -27.127591]"
        height="500"
        width="800"
      />
    </v-row>
  </div>
</template>

<script>
export default {
  name: "Home",
  data: () => ({
    token:
      "pk.eyJ1Ijoicm9kcmlnb2Z1enp5IiwiYSI6ImNrYndnbm44MjAwbjAyeXBxenY1eDFqbXMifQ.oFgG2tNZOEkJXQXnaT8Pfg",
    mapStyle: "mapbox://styles/mapbox/satellite-v9",
  }),
  components: {
    vmap: () => import("../components/Map"),
  },
};
</script>
