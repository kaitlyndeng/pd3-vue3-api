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
      default: () => ({
        scales: {
          y: {
            beginAtZero: true
          },
        }
      }),
        responsive: true,
        backgroundColor: ['#cad2c5', '#84a98c', '#52796f', '#354f52', '#2f3e46','#425057','#536066']
      }
  }
 }
,

async mounted() {
    this.loaded = false
    try {
      const res = await fetch('https://data.cityofnewyork.us/resource/m27t-ht3h.json');
      let data = await res.json()
      const year2013 = data.filter((scores)=> scores.grade === '2013')
      const year2014 = data.filter((scores)=> scores.grade === '2014')
      const year2015 = data.filter((scores)=> scores.grade === '2015')
      const year2016 = data.filter((scores)=> scores.grade === '2016')
      const year2017 = data.filter((scores)=> scores.grade === '2017')
      const year2018 = data.filter((scores)=> scores.grade === '2018')
      this.chartData.datasets[0].data = [
      year2013.length,
      year2014.length,
      year2015.length,
      year2016.length,
      year2017.length,
      year2018.length,
        ]
      this.loaded=true
    }catch(e){
      console.log(e)
    }
  }}

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