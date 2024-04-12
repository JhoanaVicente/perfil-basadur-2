<script>
    import Tabla from './lib/tabla.svelte';
    import Grafico from './lib/grafico.svelte';
    
</script>

<main>
  <Tabla />

  <Grafico />
  
</main>


<style>
  /* Estilos opcionales para el contenedor principal */
  main {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }
</style>
