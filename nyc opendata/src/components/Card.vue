<template>
  <div class="card">
    <h1>{{ math.year }}</h1>
    <h2>{{ math.grade }}</h2>
  </div>
</template>

<script>
const props = { year: Number, grade: String }
</script>

<style scoped></style>
