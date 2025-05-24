<script setup>
import Converter from './components/Converter.vue';
</script>

<template>
  <div class="content-wrapper">
    <header class="header">
      <h1 class="title">MyUnits</h1>
      <h3 class="subtitle">
        Un convertidor de unidades para todas tus necesidades, solo escoge la unidad y la cantidad, y el convertidor hará el resto.
      </h3>
    </header>

    <main>
      <Converter />
    </main>
  </div>
</template>

<style scoped>

/* Header: texto justificado al ancho del wrapper */

.title {
  text-align: center;
}
.subtitle {
  text-align: justify;
}
/* Converter heredará el 100% de ancho de .content-wrapper */
</style>
