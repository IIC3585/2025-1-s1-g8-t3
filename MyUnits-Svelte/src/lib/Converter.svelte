<script>
  import SpecificConverter from './SpecificConverter.svelte';

  // Valores iniciales
  let selectedCategory = 'longitud';
  let selectedUnitA = 'metro';
  let selectedUnitB = 'pie';

  // Magnitudes y unidades
  // Se define una unidad base para cada magnitud y se definen las conversiones a partir de esa unidad base
  const conversionTypes = {
    longitud: {
      label: 'Longitud',
      base: 'metro',
      units: {
        metro: { label: 'Metro', symbol: 'm', toBase: (x) => x, fromBase: (x) => x },
        pie: { label: 'Pie', symbol: 'ft', toBase: (x) => x / 3.28084, fromBase: (x) => x * 3.28084 },
        kilometro: { label: 'Kilómetro', symbol: 'km', toBase: (x) => x * 1000, fromBase: (x) => x / 1000 },
        milla: { label: 'Milla', symbol: 'mi', toBase: (x) => x * 1609.34, fromBase: (x) => x / 1609.34 },
        centimetro: { label: 'Centímetro', symbol: 'cm', toBase: (x) => x / 100, fromBase: (x) => x * 100 },
        pulgada: { label: 'Pulgada', symbol: 'in', toBase: (x) => x / 39.3701, fromBase: (x) => x * 39.3701 }
      }
    },
    peso: {
      label: 'Peso',
      base: 'gramo',
      units: {
        gramo: { label: 'Gramo', symbol: 'g', toBase: (x) => x, fromBase: (x) => x },
        kilogramo: { label: 'Kilogramo', symbol: 'kg', toBase: (x) => x * 1000, fromBase: (x) => x / 1000 },
        libra: { label: 'Libra', symbol: 'lb', toBase: (x) => x * 453.592, fromBase: (x) => x / 453.592 },
        onza: { label: 'Onza', symbol: 'oz', toBase: (x) => x * 28.3495, fromBase: (x) => x / 28.3495 },
        tonelada: { label: 'Tonelada', symbol: 'ton', toBase: (x) => x * 1000000, fromBase: (x) => x / 1000000 },
        miligramo: { label: 'Miligramo', symbol: 'mg', toBase: (x) => x / 1000, fromBase: (x) => x * 1000 },
      }
    },
    datos: {
      label: 'Datos',
      base: 'bytes',
      units: {
        bytes: { label: 'Byte', symbol: 'B', toBase: (x) => x, fromBase: (x) => x },
        kilobytes: { label: 'Kilobyte', symbol: 'KB', toBase: (x) => x * 1024, fromBase: (x) => x / 1024 },
        megabytes: { label: 'Megabyte', symbol: 'MB', toBase: (x) => x * (1024 ** 2), fromBase: (x) => x / (1024 ** 2) },
        gigabytes: { label: 'Gigabyte', symbol: 'GB', toBase: (x) => x * (1024 ** 3), fromBase: (x) => x / (1024 ** 3) },
      }
    },
    tiempo: {
      label: 'Tiempo',
      base: 'segundo',
      units: {
        segundo: { label: 'Segundo', symbol: 's', toBase: (x) => x, fromBase: (x) => x },
        minuto: { label: 'Minuto', symbol: 'min', toBase: (x) => x * 60, fromBase: (x) => x / 60 },
        hora: { label: 'Hora', symbol: 'h', toBase: (x) => x * 3600, fromBase: (x) => x / 3600 },
        dia: { label: 'Día', symbol: 'd', toBase: (x) => x * 86400, fromBase: (x) => x / 86400 },
      }
    },
    velocidad: {
      label: 'Velocidad',
      base: 'metro/segundo',
      units: {
        'metros/segundo': { label: 'Metro/Segundo', toBase: (x) => x, fromBase: (x) => x },
        'kilometros/hora': { label: 'Kilómetro/Hora', toBase: (x) => x / 3.6, fromBase: (x) => x * 3.6 },
        'millas/hora': { label: 'Milla/Hora', toBase: (x) => x / 2.23694, fromBase: (x) => x * 2.23694 },
      }
    },
    temperatura: {
      label: 'Temperatura',
      base: 'celcius',
      initialValue: 0,
      units: {
        celcius: { label: 'Celsius', symbol: '°C', toBase: (x) => x, fromBase: (x) => x },
        fahrenheit: { label: 'Fahrenheit', symbol: '°F', toBase: (x) => (x - 32) * 5 / 9, fromBase: (x) => x * 9 / 5 + 32 },
        kelvin: { label: 'Kelvin', symbol: 'K', toBase: (x) => x - 273.15, fromBase: (x) => x + 273.15 }
      }
    },
    energia: {
      label: 'Energía',
      base: 'julio',
      units: {
        julio: { label: 'Julio', symbol: 'J', toBase: x => x, fromBase: x => x },
        kilojulio: { label: 'Kilojulio', symbol: 'kJ', toBase: x => x * 1000, fromBase: x => x / 1000 },
        caloria: { label: 'Caloría', symbol: 'cal', toBase: x => x * 4.184, fromBase: x => x / 4.184 },
        kilocaloria: { label: 'Kilocaloría', symbol: 'kcal', toBase: x => x * 4184, fromBase: x => x / 4184 },
        'vatio-hora': { label: 'Vatio-hora', symbol: 'Wh', toBase: x => x * 3600, fromBase: x => x / 3600 },
        'electronvoltio': { label: 'Electronvoltio', symbol: 'eV', toBase: x => x * 1.60218e-19, fromBase: x => x / 1.60218e-19 }
      }
    },
    potencia: {
      label: 'Potencia',
      base: 'vatio',
      units: {
        vatio: { label: 'Vatio', symbol: 'W', toBase: x => x, fromBase: x => x },
        kilovatio: { label: 'Kilovatio', symbol: 'kW', toBase: x => x * 1000, fromBase: x => x / 1000 },
        'caballo-fuerza-hp': { label: 'Caballo de Fuerza', symbol: 'hp', toBase: x => x * 745.7, fromBase: x => x / 745.7 }
      }
    }
  };

  // Reactive declarations (Svelte's equivalent of Vue's computed properties)
  $: currentCategoryData = conversionTypes[selectedCategory];
  $: unitsList = Object.keys(currentCategoryData.units);
  
  $: unitAData = currentCategoryData.units[selectedUnitA];
  $: unitBData = currentCategoryData.units[selectedUnitB];

  $: convertAtoB = (value) => {
    if (!unitAData || !unitBData) return 0;
    const valueBase = unitAData.toBase(value);
    return unitBData.fromBase(valueBase);
  };

  $: convertBtoA = (value) => {
    if (!unitAData || !unitBData) return 0;
    const valueBase = unitBData.toBase(value);
    return unitAData.fromBase(valueBase);
  };

  $: labelA = unitAData ? unitAData.label : '';
  $: labelB = unitBData ? unitBData.label : '';
  $: initialVal = currentCategoryData?.initialValue !== undefined ? currentCategoryData.initialValue : 1;


  function onCategoryChange(event) {
    selectedCategory = event.target.value;
    // Reset units to the first two of the new category
    const newUnits = Object.keys(conversionTypes[selectedCategory].units);
    selectedUnitA = newUnits[0];
    selectedUnitB = newUnits[1] || newUnits[0]; // Fallback if only one unit
  }

</script>

<div class="converter">
  <select bind:value={selectedCategory} on:change={onCategoryChange}>
    {#each Object.entries(conversionTypes) as [key, category]}
      <option value={key}>{category.label}</option>
    {/each}
  </select>

  <select bind:value={selectedUnitA}>
    {#each unitsList as unitKey}
      <option value={unitKey}>{conversionTypes[selectedCategory].units[unitKey].label}</option>
    {/each}
  </select>

  <select bind:value={selectedUnitB}>
    {#each unitsList as unitKey}
      <option value={unitKey}>{conversionTypes[selectedCategory].units[unitKey].label}</option>
    {/each}
  </select>

  <div class="specific-converter">
    {#key selectedCategory + selectedUnitA + selectedUnitB}
        <SpecificConverter
            initialA={initialVal}
            initialB={convertAtoB(initialVal)}
            {labelA}
            {labelB}
            {convertAtoB}
            {convertBtoA}
        />
    {/key}
  </div>
</div>

<style>
  /* Styles for Converter.svelte itself are mostly global from main.css under .converter */
  /* We can add specific styles here if needed, but the Vue version didn't have scoped styles for Converter.vue */
</style>
