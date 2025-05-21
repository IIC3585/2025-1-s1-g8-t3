<script>
export default {
  data() {
    return {
      _selectedConversion: 'temperatura',
      values: {
        a: 0,
        b: 32,
      },
      conversionTypes: {
        temperatura: {
          a_value: 0,
          b_value: 32,
          labelA: 'Celsius',
          labelB: 'Fahrenheit',
          convertAtoB: (c) => (c * 9) / 5 + 32,
          convertBtoA: (f) => ((f - 32) * 5) / 9,
        },
        longitud: {
          a_value: 0,
          b_value: 0,
          labelA: 'Metros',
          labelB: 'Pies',
          convertAtoB: (m) => m * 3.28084,
          convertBtoA: (ft) => ft / 3.28084,
        },
        peso: {
          a_value: 0,
          b_value: 0,
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
    },
    selectedConversion: {
      get() {
        return this._selectedConversion;
      },
      set(value) {
        this._selectedConversion = value;
        this.values.a = this.current.a_value;
        this.values.b = this.current.b_value;
      }
    }
  },
  methods: {
    setA(event) {
      this.values.a = parseFloat(event.target.value);
      this.values.b = this.current.convertAtoB(this.values.a);
    },
    setB(event) {
      this.values.b = parseFloat(event.target.value);
      this.values.a = this.current.convertBtoA(this.values.b);
    },
  },
};
</script>

<template>
  <div class="converter">
    <select v-model="selectedConversion">
      <option v-for="(val, key) in conversionTypes" :key="key" :value="key">
        {{ key }}
      </option>
    </select>

    <div>
      <input type="number" :value="values.a" @input="setA" />
      {{ current.labelA }}
    </div>

    <p>=</p>

    <div>
      <input type="number" :value="values.b" @input="setB" />
      {{ current.labelB }}
    </div>
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