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
    <div class="specific-converter">
      <div class="field">
        <input type="number" v-model.number="valueA" />
        <span>{{ labelADisplay }}</span>
      </div>
  
      <span class="equal-sign">=</span>
  
      <div class="field">
        <input type="number" v-model.number="valueB" />
        <span>{{ labelBDisplay }}</span>
      </div>
    </div>
  </template>
  
  <style scoped>
  .specific-converter {
    display: flex;
    align-items: center;
    gap: 1rem;
  }
  
  .field {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

    .field span {
      align-self: flex-start;
    }
  
  input[type="number"] {
    width: 100%;
    padding: 0.7rem 1rem;
    font-size: 1rem;
    border: 1px solid var(--color-border);
    border-radius: 8px;
    background: var(--color-background-soft);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
    transition: border-color 0.2s, box-shadow 0.2s;
  }
  
  .equal-sign {
    font-size: 1.5rem;
    align-self: flex-start; 
  }
  </style>
