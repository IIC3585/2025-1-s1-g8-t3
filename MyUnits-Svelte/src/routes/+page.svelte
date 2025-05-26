<script>
  import Converter from '$lib/Converter.svelte';
</script>

<div class="content-wrapper">
  <header>
    <h1 class="title">MyUnits</h1>
    <h3>
      Un convertidor de unidades para todas tus necesidades, solo escoge la unidad y la cantidad, y el convertidor hará el resto.
    </h3>
  </header>

  <main>
    <Converter />
  </main>
</div>

<style>
  
  .title { 
    text-align: center; 
  }
</style>
