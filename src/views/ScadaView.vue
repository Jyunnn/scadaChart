<script setup>
import { onMounted, ref } from "vue";
import * as d3 from "d3";

let width = ref(600);
let height = ref(400);
let marginTop = ref(20);
let marginRight = ref(20);
let marginBottom = ref(30);
let marginLeft = ref(40);

// Declare the x (horizontal position) scale.
const x = d3.scaleLinear()
    .domain([0, 100])
    .range([marginLeft.value, width.value - marginRight.value]);

// Declare the y (vertical position) scale.
const y = d3.scaleLinear()
    .domain([0, 100])
    .range([height.value - marginBottom.value, marginTop.value]);

// Create the SVG container.
const svg = d3.create("svg")
    .attr("width", width.value)
    .attr("height", height.value);

// Add the x-axis.
svg.append("g")
    .attr("transform", `translate(0,${height.value - marginBottom.value})`)
    .call(d3.axisBottom(x));

// Add the y-axis.
svg.append("g")
    .attr("transform", `translate(${marginLeft.value},0)`)
    .call(d3.axisLeft(y));

svg.append("g")
.attr("transform", `translate(${width.value - marginLeft.value},0)`)
.call(d3.axisRight(y));

onMounted(()=> {
    let container = document.querySelector('#container')
    container.append(svg.node());
})

</script>

<template>
    <div id="container"></div>
</template>
