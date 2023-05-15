<template>
  <div class="card">
    <h1>School: {{ name }}</h1>
    <h2>Year: {{ year }}</h2>
    <h3>Grade: {{grade }}</h3>
  </div>
</template>

<script>
export default{
props: { 
  name: String,
  year: Number,
  grade: Number }
}

</script>

<style scoped>
.card{
  width: 60rem;
  margin: 30px auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  background-color: #cad2c5;
  color: black;
  text-align: center;
  border-radius: 30px;
}</style>
