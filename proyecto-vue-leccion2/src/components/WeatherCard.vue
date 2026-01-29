<template>
  <div class="card">
    <h3>{{ city }}</h3>
    <p><strong>Hoy:</strong> {{ today }} °C</p>
    <p><strong>Mañana:</strong> {{ tomorrow }} °C</p>
  </div>
</template>

<script>
export default {
  props: {
    city: String,
    today: Number,
    tomorrow: Number
  }
}
</script>

<style scoped>
.card {
  border: 1px solid #ddd;
  padding: 1rem;
  border-radius: 8px;
  width: 220px;
  text-align: center;
}
</style>
