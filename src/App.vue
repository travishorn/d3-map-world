<script setup>
import * as d3 from "d3";
import MapProjection from "./components/MapProjection.vue";

const projections = [
  {
    title: "Azimuthal Equal Area",
    projection: d3.geoAzimuthalEqualArea(),
  },
  {
    title: "Azimuthal Equidistant",
    projection: d3.geoAzimuthalEquidistant(),
  },
  {
    title: "Gnomonic",
    projection: d3.geoGnomonic(),
  },
  {
    title: "Orthographic",
    projection: d3.geoOrthographic(),
  },
  {
    title: "Stereographic",
    projection: d3.geoStereographic(),
  },
  {
    title: "Equal Earth",
    projection: d3.geoEqualEarth(),
  },
  {
    title: "Albers USA",
    projection: d3.geoAlbersUsa(),
  },
  {
    title: "Albers",
    projection: d3.geoAlbers(),
  },
  {
    title: "Conic Conformal",
    projection: d3.geoConicConformal(),
  },
  {
    title: "Conic Equal Area",
    projection: d3.geoConicEqualArea(),
  },
  {
    title: "Conic Equidistant",
    projection: d3.geoConicEquidistant(),
  },
  {
    title: "Equirectangular",
    projection: d3.geoEquirectangular(),
  },
  {
    title: "Mercator",
    projection: d3.geoMercator(),
  },
  {
    title: "Transverse Mercator",
    projection: d3.geoTransverseMercator(),
  },
  {
    title: "Natural Earth",
    projection: d3.geoNaturalEarth1(),
  },
];
</script>

<template>
  <div class="container">
    <MapProjection
      v-for="projection in projections"
      :key="projection.title"
      :title="projection.title"
      :projection="projection.projection"
    />
  </div>
</template>

<style>
.container {
  text-align: center;
  margin: 4rem auto;
  width: 600px;
}
</style>
