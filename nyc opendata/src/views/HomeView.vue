<template>
  <div class="container">
    <h1>2013-2018 School Math Results</h1>
    <!-- <Card v-for /> -->
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import Card from '../components/Card.vue'
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

<style lang="scss" scoped></style>
