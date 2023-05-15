<template>
  <h1>2013-2018 School Math Results</h1>
  <div class="container">
    <Card v-for= "scores in scores" 
    :key="scores.school_name"
    :name="scores.school_name"
    :grade = "scores.grade"
    :year="scores.year"/>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Card from '../components/Card.vue'

const scores = ref('')
async function getData() {
  let res = await fetch("https://data.cityofnewyork.us/resource/m27t-ht3h.json")
  let data = await res.json()
  scores.value = data
}
onMounted(() => {
  getData()
})
</script>

<style scoped>
.h1{
  text-align: center;
}

</style>
