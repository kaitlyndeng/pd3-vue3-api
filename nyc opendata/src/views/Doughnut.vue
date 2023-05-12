<template>
  <div class="container">
    <Doughnut v-if="loaded" :data="chartData" />
  </div>
</template>

<script>
import { Doughnut } from 'vue-chartjs'
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
export default {
  name: 'DoughnutChart',
  components: { Doughnut },
  props: {},
  data() {
    return {
      load: false,
      chartData: null,
      chartOptions: {
        responsive: true
      }
    }
  },
  async mounted() {
    this.loaded = false

    try {
      const { data } = await fetch('https://data.cityofnewyork.us/resource/m27t-ht3h.json')
      this.chartdata = data

      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}
</script>
