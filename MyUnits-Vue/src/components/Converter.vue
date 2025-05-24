<script>
import SpecificConverter from './SpecificConverter.vue';

export default {
  components: {
    SpecificConverter
  },
  data() {
    return {
      // Valores iniciales
      selectedCategory: 'longitud',
      selectedUnitA: 'metro',
      selectedUnitB: 'pie',
      // Magnitudes y unidades
      // Se define una unidad base para cada magnitud y se definen las conversiones a partir de esa unidad base
      conversionTypes: {
        longitud: {
          label: 'Longitud',
          base: 'metro',
          units: {
            metro: {
              label: 'Metro',
              symbol: 'm',
              toBase: (x) => x,
              fromBase: (x) => x
            },
            pie: {
              label: 'Pie',
              symbol: 'ft',
              toBase: (x) => x / 3.28084,
              fromBase: (x) => x * 3.28084
            },
            kilometro: {
              label: 'Kilómetro',
              symbol: 'km',
              toBase: (x) => x * 1000,
              fromBase: (x) => x / 1000
            },
            milla: {
              label: 'Milla',
              symbol: 'mi',
              toBase: (x) => x * 1609.34,
              fromBase: (x) => x / 1609.34
            },
            centimetro: {
              label: 'Centímetro',
              symbol: 'cm',
              toBase: (x) => x / 100,
              fromBase: (x) => x * 100
            },
            pulgada: {
              label: 'Pulgada',
              symbol: 'in',
              toBase: (x) => x / 39.3701,
              fromBase: (x) => x * 39.3701
            }
          }
        },
        peso: {
          label: 'Peso',
          base: 'gramo',
            units: {
              gramo: {
                label: 'Gramo',
                symbol: 'g',
                toBase: (x) => x,
                fromBase: (x) => x
              },
              kilogramo: {
                label: 'Kilogramo',
                symbol: 'kg',
                toBase: (x) => x * 1000,
                fromBase: (x) => x / 1000
              },
              libra: {
                label: 'Libra',
                symbol: 'lb',
                toBase: (x) => x * 453.592,
                fromBase: (x) => x / 453.592
              },
              onza: {
                label: 'Onza',
                symbol: 'oz',
                toBase: (x) => x * 28.3495,
                fromBase: (x) => x / 28.3495
              },
              tonelada: {
                label: 'Tonelada',
                symbol: 'ton',
                toBase: (x) => x * 1000000,
                fromBase: (x) => x / 1000000
              },
              miligramo: {
                label: 'Miligramo',
                symbol: 'mg',
                toBase: (x) => x / 1000,
                fromBase: (x) => x * 1000
              },
            },
        },
        datos: {
          label: 'Datos',
          base: 'bytes',
          units: {
            bytes: {
              label: 'Bytes',
              symbol: 'B',
              toBase: (x) => x,
              fromBase: (x) => x
            },
            kilobytes: {
              label: 'Kilobytes',
              symbol: 'KB',
              toBase: (x) => x * 1024,
              fromBase: (x) => x / 1024
            },
            megabytes: {
              label: 'Megabytes',
              symbol: 'MB',
              toBase: (x) => x * (1024 ** 2),
              fromBase: (x) => x / (1024 ** 2)
            },
            gigabytes: {
              label: 'Gigabytes',
              symbol: 'GB',
              toBase: (x) => x * (1024) ** 3,
              fromBase: (x) => x / (1024 ** 3)
            },
          },
        },
        tiempo: {
          label: 'Tiempo',
          base: 'segundo',
          units: {
            segundo: {
              label: 'Segundo',
              symbol: 's',
              toBase: (x) => x,
              fromBase: (x) => x
            },
            minuto: {
              label: 'Minuto',
              symbol: 'min',
              toBase: (x) => x * 60,
              fromBase: (x) => x / 60
            },
            hora: {
              label: 'Hora',
              symbol: 'h',
              toBase: (x) => x * 3600,
              fromBase: (x) => x / 3600
            },
            dia: {
              label: 'Día',
              symbol: 'd',
              toBase: (x) => x * 86400,
              fromBase: (x) => x / 86400
            },
          }
        },
        velocidad: {
          label: 'Velocidad',
          base: 'metros/segundo',
          units: {
            'metros/segundo': {
              label: 'Metros/Segundo',
              toBase: (x) => x,
              fromBase: (x) => x
            },
            'kilometros/hora': {
              label: 'Kilómetros/Hora',
              toBase: (x) => x / 3.6,
              fromBase: (x) => x * 3.6
            },
            'millas/hora': {
              label: 'Millas/Hora',
              toBase: (x) => x / 2.23694,
              fromBase: (x) => x * 2.23694
            },
          },
        },
        temperatura: {
          label: 'Temperatura',
          base: 'celcius',
          initialValue: 0,
          units: {
            celcius: {
              label: 'Celsius',
              symbol: '°C',
              toBase: (x) => x,
              fromBase: (x) => x
            },
            fahrenheit: {
              label: 'Fahrenheit',
              symbol: '°F',
              toBase: (x) => (x - 32) * 5 / 9,
              fromBase: (x) => x * 9 / 5 + 32
            },
            kelvin: {
              label: 'Kelvin',
              symbol: 'K',
              toBase: (x) => x - 273.15,
              fromBase: (x) => x + 273.15
            },
          }
        },
        energia: {
          label: 'Energía',
          base: 'joule',
          units: {
            julio: {
              label: 'Joule',
              symbol: 'J',
              toBase: (x) => x,
              fromBase: (x) => x
            },
            kilojulio: {
              label: 'Kilojoule',
              symbol: 'kJ',
              toBase: (x) => x * 1000,
              fromBase: (x) => x / 1000
            },
            caloría: {
              label: 'Caloría',
              symbol: 'cal',
              toBase: (x) => x * 4.184,
              fromBase: (x) => x / 4.184
            },
            kilocaloría: {
              label: 'Kilocaloría',
              symbol: 'kcal',
              toBase: (x) => x * 4184,
              fromBase: (x) => x / 4184
            },
            wattHora: {
              label: 'Watt-Hora',
              symbol: 'Wh',
              toBase: (x) => x * 3600,
              fromBase: (x) => x / 3600
            },
            electronvolt: {
              label: 'Electronvolt',
              symbol: 'eV',
              toBase: (x) => x * 1.60218e-19,
              fromBase: (x) => x / 1.60218e-19
            },
          }
        },
        potencia: {
          label: 'Potencia',
          base: 'watt',
          units: {
            watt: {
              label: 'Watt',
              symbol: 'W',
              toBase: (x) => x,
              fromBase: (x) => x
            },
            kilowatt: {
              label: 'Kilowatt',
              symbol: 'kW',
              toBase: (x) => x * 1000,
              fromBase: (x) => x / 1000
            },
            caballoFuerza: {
              label: 'Caballo de Fuerza',
              symbol: 'hp',
              toBase: (x) => x * 745.7,
              fromBase: (x) => x / 745.7
            },
          }
        }
      }
    };
  },
  computed: {
    currentCategory() {
      return this.conversionTypes[this.selectedCategory];
    },
    unitsList() {
      return Object.keys(this.currentCategory.units);
    },
    unitA() {
      return this.currentCategory.units[this.selectedUnitA];
    },
    unitB() {
      return this.currentCategory.units[this.selectedUnitB];
    },
    convertAtoB() {
      return (value) => this.unitB.fromBase(this.unitA.toBase(value));
    },
    convertBtoA() {
      return (value) => this.unitA.fromBase(this.unitB.toBase(value));
    },
    labelA() {
      return this.unitA.label;
    },
    labelB() {
      return this.unitB.label;
    },
    initialValue() {
      return this.currentCategory.initialValue? this.currentCategory.initialValue : 1;
    }
  },
  methods: {
    onCategoryChange(event) {
      this.selectedCategory = event.target.value;
      const units = Object.keys(this.conversionTypes[this.selectedCategory].units);
      this.selectedUnitA = units[0];
      this.selectedUnitB = units[1] || units[0];
    }
  }
};
</script>

<template>
  <div class="converter">
    <!-- Selector de magnitud -->
    <select :value="selectedCategory" @change="onCategoryChange">
      <option v-for="(category, key) in conversionTypes" :key="key" :value="key">
        {{ category.label }}
      </option>
    </select>

    <!-- Selector de unidad 1 -->
    <select v-model="selectedUnitA">
      <option v-for="unit in unitsList" :key="unit" :value="unit">
        {{ currentCategory.units[unit].label }} ({{ currentCategory.units[unit].symbol }})
      </option>
    </select>

    <!-- Selector de unidad 2 -->
    <select v-model="selectedUnitB">
      <option v-for="unit in unitsList" :key="unit" :value="unit">
        {{ currentCategory.units[unit].label }} ({{ currentCategory.units[unit].symbol }})
      </option>
    </select>

    <!-- Convertidor específico -->
    <SpecificConverter
      :key="selectedUnitA + '-' + selectedUnitB"
      :initialA="initialValue"
      :initialB="convertAtoB(initialValue)"
      :labelA="labelA"
      :labelB="labelB"
      :convertAtoB="convertAtoB"
      :convertBtoA="convertBtoA"
    />
  </div>
</template>