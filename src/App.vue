<script setup lang="js">
import { ref } from "vue";
import "./main.css";


const container = ref(null);
const relativeX = ref(0);
const relativeY = ref(0);


const percentX = ref(0);
const percentY = ref(0);

const containerMouseOver = (event) => {
  const rect = container.value.getBoundingClientRect();
  relativeX.value = event.clientX - rect.left;
  relativeY.value = event.clientY - rect.top;

  // As percentage of element size
  percentX.value = Math.round((relativeX.value / rect.width) * 10000) / 100;
  percentY.value = Math.round((relativeY.value / rect.width) * 10000) / 100;
}


</script>


<template>
  <p> relative x: {{ relativeX }} </p>
  <p> relative y: {{ relativeY }} </p>
  <p> percent x: {{ percentX }} </p>
  <p> percent y: {{ percentY }} </p>

  <div ref="container" @mousemove="containerMouseOver" class="w-56 h-56 bg-amber-300 text-5xl"> </div>

</template>

<style scoped></style>
