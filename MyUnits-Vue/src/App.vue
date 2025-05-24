<script setup>
import Converter from './components/Converter.vue';


</script>

<template>
  <header>
    <div class="wrapper">
      <h1>MyUnits</h1>
      <p>
        Un convertidor de unidades para todas tus necesidades.
      </p>
      <p>
        Solo selecciona tu magnitud y luego las unidades que deseas convertir.
        <br />
        El convertidor se encargará del resto.
        <br />
      </p>
    </div>
  </header>

  <main>
    <Converter />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    flex-direction: column;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
