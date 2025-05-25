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
            b: this.initialB
        }
    },
    computed: {
        displayLabelA() {
            return this.getPluralizedLabel(this.labelA, this.a);
        },
        displayLabelB() {
            return this.getPluralizedLabel(this.labelB, this.b);
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
        },
        getPluralizedLabel(label, value) {
            const numValue = parseFloat(value);
            if (numValue === 1) {
                return label; 
            } else {
                if (label.includes("/")) {
                    return label.replace("/", "s/"); 
                }
                else {
                    return label
                }
            }
        }
    }
}
</script>

<template>
    <div>
        <div>
      <input type="number" :value="a" @input="onInputA" />
      {{ displayLabelA }}
    </div>

    <p>=</p>

    <div>
      <input type="number" :value="b" @input="onInputB" />
      {{ displayLabelB }}
    </div>
  </div>
</template>
