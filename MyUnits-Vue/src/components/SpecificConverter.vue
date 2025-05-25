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
            valueA: Number(this.initialA),
            valueB: Number(this.initialB),
            labelADisplay: '',
            labelBDisplay: ''
        }
    },
    watch: {
        valueA: {
            immediate: true,
            handler(newVal) {
                this.labelADisplay = this.getPluralizedLabel(this.labelA, newVal);
                // Only update B if A changed by user input, not by the conversion from B
                if (!this.updatingFromB) {
                    this.updatingFromA = true;
                    this.valueB = this.convertAtoB(Number(newVal));
                    this.$nextTick(() => {
                        this.updatingFromA = false;
                    });
                }
            }
        },
        valueB: {
            immediate: true,
            handler(newVal) {
                this.labelBDisplay = this.getPluralizedLabel(this.labelB, newVal);
                // Only update A if B changed by user input, not by the conversion from A
                if (!this.updatingFromA) {
                    this.updatingFromB = true;
                    this.valueA = this.convertBtoA(Number(newVal));
                    this.$nextTick(() => {
                        this.updatingFromB = false;
                    });
                }
            }
        }
    },
    created() {
        // Initialize flags to prevent circular updates
        this.updatingFromA = false;
        this.updatingFromB = false;
    },
    methods: {
        getPluralizedLabel(label, value) {
            const numValue = Number(value);
            if (numValue === 1) {
                return label; 
            } else {
                if (label.includes("/")) {
                    return label.replace("/", "s/"); 
                }
                else if (label.includes("Caballo")) {
                    return label.replace("Caballo", "Caballos")
                }
                else {
                    return label + "s";
                }
            }
        }
    }
}
</script>

<template>
    <div>
        <div>
      <input type="number" v-model.number="valueA" />
      {{ labelADisplay }}
    </div>

    <p>=</p>

    <div>
      <input type="number" v-model.number="valueB" />
      {{ labelBDisplay }}
    </div>
  </div>
</template>
