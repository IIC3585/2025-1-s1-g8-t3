<script>
import SpecificConverter from './SpecificConverter.vue';
export default {
  components: {
    SpecificConverter
  },
  data() {
    return {
      selectedCategory: 'temperatura',
      selectedConversionKey: 'Celsius - Fahrenheit',
      conversionTypes: {
        temperatura: {
          label: 'Temperatura',
          conversions: {
            "Celsius - Fahrenheit": {
              initialA: 0,
              initialB: 32,
              labelA: 'Celsius',
              labelB: 'Fahrenheit',
              convertAtoB: (c) => (c * 9) / 5 + 32,
              convertBtoA: (f) => ((f - 32) * 5) / 9,
            },
          },
        },
        longitud: {
          label: 'Longitud',
          conversions: {
            "Metros - Pies": {
              initialA: 0,
              labelA: 'Metros',
              labelB: 'Pies',
              convertAtoB: (m) => m * 3.28084,
              convertBtoA: (ft) => ft / 3.28084,
            },
          },
        },
        peso: {
          label: 'Peso',
          conversions: {
            "Kilogramos - Libras": {
              initialA: 0,
              labelA: 'Kilogramos',
              labelB: 'Libras',
              convertAtoB: (kg) => kg * 2.20462,
              convertBtoA: (lb) => lb / 2.20462,
            },
          },
        },
        datos: {
          label: 'Datos',
          conversions: {
            "Bytes - Kilobytes": {
              initialA: 0,
              labelA: 'Bytes',
              labelB: 'Kilobytes',
              convertAtoB: (b) => b / 1024,
              convertBtoA: (kb) => kb * 1024,
            },
            "Kilobytes - Megabytes": {
              initialA: 0,
              labelA: 'Kilobytes',
              labelB: 'Megabytes',
              convertAtoB: (kb) => kb / 1024,
              convertBtoA: (Mb) => Mb * 1024,
            },
            "Megabytes - Gigabytes": {
              initialA: 0,
              labelA: 'Megabytes',
              labelB: 'Gigabytes',
              convertAtoB: (Mb) => Mb / 1024,
              convertBtoA: (Gb) => Gb * 1024,
            },
          },
        },
        tiempo: {
          label: 'Tiempo',
          conversions: {
            "Segundos - Minutos": {
              initialA: 0,
              labelA: 'Segundos',
              labelB: 'Minutos',
              convertAtoB: (sec) => sec / 60,
              convertBtoA: (min) => min * 60,
            },
            "Minutos - Horas": {
              initialA: 0,
              labelA: 'Minutos',
              labelB: 'Horas',
              convertAtoB: (min) => min / 60,
              convertBtoA: (hr) => hr * 60,
            },
          },
        },
        velocidad: {
          label: 'Velocidad',
          conversions: {
            "Metros/Segundo - Kilometro/Hora": {
              initialA: 0,
              labelA: 'Metros/Segundo',
              labelB: 'Kilometro/Hora',
              convertAtoB: (ms) => ms * 3.6,
              convertBtoA: (kmh) => kmh / 3.6,
            },
          },
        },
      }
    };
  },
  computed: {
    currentConversions() {
    const category = this.conversionTypes[this.selectedCategory];
    return category ? category.conversions : {};
    },
    current() {
      const conversion = this.currentConversions[this.selectedConversionKey];
      return conversion ? conversion : {};
    }
  },
  methods: {
    onCategoryChange(event) {
      const newCategory = event.target.value;
      this.selectedCategory = newCategory;

      const conversions = this.conversionTypes[newCategory].conversions;
      const firstKey = Object.keys(conversions)[0];
      this.selectedConversionKey = firstKey;
    }
  },
};
</script>

<template>
  <div class="converter">
    <select :value="selectedCategory" @change="onCategoryChange">
      <option v-for="(category, key) in conversionTypes" :key="key" :value="key">
        {{ category.label }}
      </option>
    </select>

    <select v-model="selectedConversionKey">
      <option
        v-for="(conversion, key) in currentConversions"
        :key="key"
        :value="key"
      >
        {{ key }}
      </option>
    </select>

    <SpecificConverter
      :key="selectedConversionKey"
      :initialA="current.initialA"
      :initialB="current.initialB"
      :labelA="current.labelA"
      :labelB="current.labelB"
      :convertAtoB="current.convertAtoB"
      :convertBtoA="current.convertBtoA"
    />
  </div>
</template>