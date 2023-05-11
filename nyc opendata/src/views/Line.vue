<template>
  <div class="about">
    <h1></h1>
    <Line v-if="loaded" :data="chartData" />
  </div>
</template>
<script>
import { ref, onMounted } from 'vue'
import { Line } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

const math = ref('')
async function getData() {
  let res = await fetch('https://data.cityofnewyork.us/resource/m27t-ht3h.json')
  let data = await res.json()
  math.value = data.results
}
onMounted(() => {
  getData()
})
</script>
<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
