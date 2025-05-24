<script>
export default {
    name: 'SpecificConverter',
    props: {
        initialA: {
            type: Number,
            required: true
        },
        initialB: {
            type: Number,
            required: true
        },
        labelA: {
            type: String,
            required: true
        },
        labelB: {
            type: String,
            required: true
        },
        convertAtoB: {
            type: Function,
            required: true
        },
        convertBtoA: {
            type: Function,
            required: true
        }
    },
    data() {
        return {
            a: this.initialA,
            b: this.initialB || this.initialA
        }
    },
    methods: {
        onInputA(event) {
            this.a = event.target.value;
            this.b = this.convertAtoB(this.a);
        },
        onInputB(event) {
            this.b = event.target.value;
            this.a = this.convertBtoA(this.b);
        }
    }
}
</script>

<template>
    <div>
        <div>
      <input type="number" :value="a" @input="onInputA" />
      {{ labelA }}
    </div>

    <p>=</p>

    <div>
      <input type="number" :value="b" @input="onInputB" />
      {{ labelB }}
    </div>
  </div>
</template>
