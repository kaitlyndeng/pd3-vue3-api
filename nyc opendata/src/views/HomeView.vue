<template>
  <div></div>
</template>

<script>
import { ref, onMounted } from 'vue'
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

<style scoped></style>
