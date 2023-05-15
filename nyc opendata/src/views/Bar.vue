<template>
  <div class="bar">
    <h1>Students Tested Per Year</h1>
    <Pie v-if="loaded" :data="chartData" :options="chartOptions" />
  </div>
</template>
<script>
import { Bar } from 'vue-chartjs'
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

export default{
  name: 'BarChart',
  components: { Bar },
 data (){
  return{
    loaded: false,
      chartData:{
        labels: [
        '2013',
          '2014',
          '2015',
          '2016',
          '2017',
          '2018',
          ],
        datasets: [{ data: [] }]} ,
      chartOptions: {
        responsive: true
      }
  }
 }
}
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