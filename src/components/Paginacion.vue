<script setup>
// defineprops propermite usar la variables rectivas
defineProps(["Inicio", "Fin", "maxLength"]);

// se una defineEmits si no se quiere usar el signo $ antes del emit,
const emit = defineEmits(["sgt", "rtn"]);
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <!-- <button
      @click="emit('rtn')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="Inicio === 0"
    > -->

    <button
      @click="emit('rtn')"
      type="button"
      class="btn btn-outline-primary"
    >
      Retroceder {{ Inicio }}
    </button>

    <!-- <button
      @click="$emit('sgt')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="Fin >= maxLength"
    > -->
    <button
      @click="$emit('sgt')"
      type="button"
      class="btn btn-outline-primary"
    >
      Siguiente {{ Fin }}
    </button>
  </div>
</template>
