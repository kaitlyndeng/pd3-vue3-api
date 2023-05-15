<template>
  <h1>Students Tested Per Grade</h1>
  <div class="container">
    <Doughnut v-if="loaded" :data="chartData" :options="chartOptions"/>
  </div>
</template>

<script>
import { Doughnut } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Tooltip,
  Legend,
  ArcElement,
} from 'chart.js'

ChartJS.register(Tooltip, Legend, ArcElement)

export default {
  name: "DoughnutChart",
  components: { Doughnut },
  data() {
    return {
      loaded: false,
      chartData:{
        labels: [
            '3rd Grade',
            '4th Grade',
            '5th Grade',
            '6th Grade',
            '7th Grade',
            '8th Grade',
            'All Grades'
          ],
        datasets: [{ data: [] }]} ,
      chartOptions: {
        responsive: true,
        backgroundColor: ['#cad2c5', '#84a98c', '#52796f', '#354f52', '#2f3e46','#425057','#536066']
      }
    }
  },
  async mounted() {
    this.loaded = false
    try {
      const res = await fetch('https://data.cityofnewyork.us/resource/m27t-ht3h.json');
      let data = await res.json()
      const grade3 = data.filter((scores)=> scores.grade === '3')
      const grade4 = data.filter((scores)=> scores.grade === '4')
      const grade5 = data.filter((scores)=> scores.grade === '5')
      const grade6 = data.filter((scores)=> scores.grade === '6')
      const grade7 = data.filter((scores)=> scores.grade === '7')
      const grade8 = data.filter((scores)=> scores.grade === '7')
      const allGrades = data.filter((scores)=> scores.grade === 'All Grades')
      this.chartData.datasets[0].data = [
          grade3.length,
          grade4.length,
          grade5.length,
          grade6.length,
          grade7.length,
          grade8.length,
          allGrades.length
        ]
        // this.chartOptions.backgroundColor = ['#cad2c5', '#84a98c', '#52796f', '#354f52', '#2f3e46','#425057','#536066']
      this.loaded=true
    } catch(e){
      console.log(e)
    }
    
  }
}
</script>
