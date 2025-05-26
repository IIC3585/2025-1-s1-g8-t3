<script>
  export let initialA;
  export let labelA;
  export let labelB;
  export let convertAtoB;
  export let convertBtoA;

  let valueA = Number(initialA);
  let valueB = convertAtoB(Number(initialA));

  $: labelADisplay = getPluralizedLabel(labelA, valueA);
  $: labelBDisplay = getPluralizedLabel(labelB, valueB);

  var isUpdatingProgrammatically = false;

  function handleInputA(event) {
    if (isUpdatingProgrammatically) return;

    const newA = Number(event.target.value);
    valueA = newA; 

    isUpdatingProgrammatically = true;
    valueB = convertAtoB(newA); 

    Promise.resolve().then(() => {
      isUpdatingProgrammatically = false;
    });
  }

  function handleInputB(event) {
    if (isUpdatingProgrammatically) return;

    const newB = Number(event.target.value);
    valueB = newB;

    isUpdatingProgrammatically = true;
    valueA = convertBtoA(newB);

    Promise.resolve().then(() => {
      isUpdatingProgrammatically = false;
    });
  }
  
  function getPluralizedLabel(label, value) {
    const numValue = Number(value);
    if (numValue === 1) {
      return label; 
    } else {
      if (label.includes("/")) {
        return label.replace("/", "s/"); 
      } else if (label.includes("Caballo")) {
        return label.replace("Caballo", "Caballos")
      } else {
        return label + "s";
      }
    }
  }
</script>

<div>
  <div>
    <input type="number" value={valueA} on:input={handleInputA} />
    {labelADisplay}
  </div>

  <p>=</p>

  <div>
    <input type="number" value={valueB} on:input={handleInputB} />
    {labelBDisplay}
  </div>
</div>

<style>
  div {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    align-items: center;
    gap: 0.5rem; 
    width: 100%;
  }

  div > div {
    display: flex; 
    flex-direction: column; 
    align-items: flex-start; 
    gap: 0.25rem; 
  }

  input {
    width: 100%; 
  }
  
  p {
    text-align: center;
    font-weight: bold;
    font-size: 1.2rem;
    margin: 0; 
  }

   div > div > :not(input) { 
    font-size: 0.9rem;
    color: var(--color-text);
    padding-left: 0.2rem; 
  }
</style>
