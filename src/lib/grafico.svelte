<script>
  let styles = [
    { name: 'Generador', x: 50, y: 10 },
    { name: 'Implementador', x: 90, y: 50 },
    { name: 'Optimizador', x: 50, y: 90 },
    { name: 'Finalizador', x: 10, y: 50 }
  ];
</script>

<style>
  .cross {
    position: relative;
    width: 100px;
    height: 100px;
  }
  .style-point {
    position: absolute;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: blue;
  }
  .line {
    position: absolute;
    border: 1px solid blue;
  }
</style>

<div class="cross">
  {#each styles as style}
    <div class="style-point" style="left: {style.x}%; top: {style.y}%;"></div>
  {/each}
  <div class="line" style="left: 0; top: 50%; width: 100%;"></div>
  <div class="line" style="left: 50%; top: 0; height: 100%;"></div>
</div>
