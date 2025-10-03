<script setup lang="js">
import { ref } from "vue";
import "./main.css";


const container = ref(null);
const mouseStatus = ref(false);
const relativeX = ref(0);
const relativeY = ref(0);
const percentX = ref(0);
const percentY = ref(0);

const containerMouseMove = (event) => {
  const rect = container.value.getBoundingClientRect();
  relativeX.value = event.clientX - rect.left;
  relativeY.value = event.clientY - rect.top;
  percentX.value = Math.round((relativeX.value / rect.width) * 10000) / 100;
  percentY.value = Math.round((relativeY.value / rect.width) * 10000) / 100;
}

const containerMouseEnter = () => { mouseStatus.value = true }
const containerMouseLeave = () => { mouseStatus.value = false }

const notes = [12, 24, 5, 75, 33, 95, 50, 80];


</script>


<template>
  <p> relative x: {{ relativeX }} </p>
  <p> relative y: {{ relativeY }} </p>
  <p> percent x: {{ percentX }} </p>
  <p> percent y: {{ percentY }} </p>
  <p> mouse status: {{ mouseStatus }} </p>


  <div ref="container" @mousemove="containerMouseMove" @mouseenter="containerMouseEnter"
    @mouseleave="containerMouseLeave" class="flex items-center w-full h-56 bg-amber-300 text-5xl">
    <div v-for="(note, index) in notes" :key="index" class="note" :style="{ left: `${note}%` }">
      <div>child</div>
    </div>
    <div ref="sub-container" class="sub-container w-full h-2 bg-blue-500 "> </div>
  </div>

</template>

<style scoped>
.note {
  position: absolute;
  width: 2px;
  height: 20px;
  background: var(--color-blue-500);
  /* border-radius: 50%; */
  /* Center the dot on the position */
  transform: translateX(-50%);
  transform: translateY(-50%);
}

.sub-container {
  transition: transform 0.3s ease;
}

.sub-container:hover {
  transform: scaleY(2);
}
</style>
