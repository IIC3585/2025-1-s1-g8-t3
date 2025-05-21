<script>
import SpecificConverter from './SpecificConverter.vue';
export default {
    components: {
        SpecificConverter
    },
  data() {
    return {
      // Getter y Setter de tipo de conversion para actualizar también los valores de los inputs
      selectedConversion: 'temperatura',
      conversionTypes: {
        temperatura: {
          initialA: 0,
          initialB: 32,
          labelA: 'Celsius',
          labelB: 'Fahrenheit',
          convertAtoB: (c) => (c * 9) / 5 + 32,
          convertBtoA: (f) => ((f - 32) * 5) / 9,
        },
        longitud: {
          initialA: 0,
          initialB: 0,
          labelA: 'Metros',
          labelB: 'Pies',
          convertAtoB: (m) => m * 3.28084,
          convertBtoA: (ft) => ft / 3.28084,
        },
        peso: {
          initialA: 0,
          initialB: 0,
          labelA: 'Kilogramos',
          labelB: 'Libras',
          convertAtoB: (kg) => kg * 2.20462,
          convertBtoA: (lb) => lb / 2.20462,
        }
      },
    };
  },
  computed: {
    current() {
      return this.conversionTypes[this.selectedConversion];
    }
  }
};
</script>

<template>
  <div class="converter">
    <select v-model="selectedConversion">
      <option v-for="(val, key) in conversionTypes" :key="key" :value="key">
        {{ key }}
      </option>
    </select>

    <SpecificConverter
      :key="selectedConversion"
      :initialA="current.initialA"
      :initialB="current.initialB"
      :labelA="current.labelA"
      :labelB="current.labelB"
      :convertAtoB="current.convertAtoB"
      :convertBtoA="current.convertBtoA"
    />
  </div>
</template>

<style scoped>
.converter {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}
input {
  width: 120px;
  padding: 0.4rem;
}
select {
  padding: 0.4rem;
}
</style>