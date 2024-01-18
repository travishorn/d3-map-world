<script setup>
import { defineProps, onMounted } from "vue";
import * as d3 from "d3";
import geoData from "../continents.json";

const props = defineProps({
  title: String,
  projection: Function,
});

const id = crypto.randomUUID();

onMounted(() => {
  const svg = d3.select(`#map_${id}`);
  const width = svg.attr("width");
  const height = svg.attr("height");
  const margin = { top: 10, right: 10, bottom: 10, left: 10 };
  const graticuleGenerator = d3.geoGraticule();
  const graticules = graticuleGenerator();
  const projection = props.projection;
  const geoGenerator = d3.geoPath().projection(projection);
  const map = svg.append("g")
    .attr("transform", `translate(${margin.left} ${margin.top})`);

  projection.fitSize(
    [width - margin.left - margin.right, height - margin.top - margin.bottom],
    geoData,
  );

  map.selectAll(".boundary")
    .data(geoData.features)
    .join("path")
    .attr("class", "boundary")
    .attr("d", geoGenerator)
    .attr("fill", "none")
    .attr("stroke", "mediumseagreen");

  map.append("path")
    .attr("d", geoGenerator(graticules))
    .attr("fill", "none")
    .attr("stroke", "white")
    .attr("opacity", 0.1);

  d3.range(-180, 180 + 1, 10).forEach((x) => {
    map.append("text")
      .attr("transform", `translate(${projection([x, 0])})`)
      .attr("fill", "white")
    .attr("opacity", 0.5)
      .attr("font-size", 10)
      .attr("text-anchor", "middle")
      .text(x);
  });

  d3.range(-90, 90 + 1, 10).forEach((y) => {
    map.append("text")
      .attr("transform", `translate(${projection([0, y])})`)
      .attr("fill", "white")
      .attr("opacity", 0.5)
      .attr("font-size", 10)
      .attr("text-anchor", "end")
      .attr("alignment-baseline", "middle")
      .text(y);
  });
});
</script>

<template>
  <div class="container">
    <h2>{{ title }}</h2>
    <svg :id="`map_${id}`" width="600" height="600"></svg>
  </div>
</template>

<style scoped>
.container {
  margin: 6rem 0;
}

svg {
  background: #212121;
  border-radius: 10px;
}
</style>
