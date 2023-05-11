<template>
  <div class="container">
    <h1>2013-2018 School Math Results</h1>
    <Doughnut v-if="loaded" :data="chartData" />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
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
  props: {
    chartData: {
      type: Object,
      required: true
    },
    chartOptions: {
      type: Object,
      default: () => {}
    }
  }
}
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
