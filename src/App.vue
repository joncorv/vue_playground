<script setup lang="js">
import { ref } from "vue";
import "./main.css";


const myContainer = ref(null);
const mouseStatus = ref(false);
const relativeX = ref(0);
const relativeY = ref(0);
const percentX = ref(0);
const percentY = ref(0);

const containerMouseMove = (event) => {
  const rect = myContainer.value.getBoundingClientRect();
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


  <div ref="myContainer" class="myContainer" @mousemove="containerMouseMove" @mouseenter="containerMouseEnter"
    @mouseleave="containerMouseLeave">
    <div v-for="(note, index) in notes" :key="index" class="note" :style="{ left: `${note}%` }">
      <div class="child">{{ index }}</div>
    </div>
    <div ref="sub-container" class="sub-container w-full h-2 bg-blue-500 "> </div>
  </div>



</template>

<style scoped>
.myContainer {
  position: fixed;
  margin: 1rem;
  width: calc(100vw - 2rem);
  height: 8rem;
  display: flex;
  background-color: hsl(0, 0%, 25%);
  align-items: center;
  border-radius: 25px;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 2px 4px rgba(0, 0, 0, 0.6);
}

.child {
  transform: translate(-150%, -150%);
  font-size: var(--text-sm);
}

.sub-container {
  transition: transform 0.1s ease;
}

.sub-container:hover {
  transform: scaleY(2);
}

.note {
  position: absolute;
  width: 2px;
  height: 20px;
  background: var(--color-blue-500);
  transform: translateX(-50%);
  transform: translateY(-50%);
  z-index: 1;
  margin: 1rem;
}
</style>

<style>
/* body { */
/*   background-color: hsl(0, 0, 10%); */
/* } */

/* * { */
/*   margin: 0; */
/*   padding: 0; */
/*   box-sizing: border-box; */
/* } */
</style>
