<script setup>
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: "Sin descripción",
  },
});
</script>

<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ id }} - {{ title }}</h5>
      <p class="card-text">{{ body }}</p>
      <button @click="$emit('CambiarFavoritoFetch', id)" class="btn btn-outline-primary">Favorito</button>
    </div>
  </div>
</template>
