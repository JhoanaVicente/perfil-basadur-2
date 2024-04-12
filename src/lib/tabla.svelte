<script>
    let results = [0, 0, 0, 0]; // Inicializa los resultados de las cuatro columnas
    const excludedRows = new Set([1, 2, 5, 10, 14, 17]); // Define las filas que se excluyen del cálculo
    let totalResults = 0; // Variable para almacenar el total de resultados
  
    function handleChange(columnIndex, rowIndex, value) {
      // Verifica si la fila actual está en la lista de filas excluidas
      if (!excludedRows.has(rowIndex + 1)) {
        results[columnIndex] += value; // Actualiza el resultado de la columna
      }
      totalResults = results.reduce((acc, columnTotal) => acc + columnTotal, 0); // Calcula el total de resultados
    }
  </script>
  
  {#each [0, 1, 2, 3] as columnIndex}
    <div class="column">
      <h2>Columna {columnIndex + 1}</h2>
      {#each Array.from({ length: 18 }).map((_, rowIndex) => rowIndex) as rowIndex}
        <div class="row">
          <span>Palabra {rowIndex + 1}</span>
          <select on:change={(event) => handleChange(columnIndex, rowIndex, +event.target.value)}>
            {#each [0, 1, 2, 3, 4] as value}
              <option value={value}>{value}</option>
            {/each}
          </select>
        </div>
      {/each}
    </div>
  {/each}
  
  <h2>Resultados:</h2>
  {#each results as result, index}
    <p>Columna {index + 1}: {result}</p>
  {/each}
  
  <h2>Total: {totalResults}</h2>
  
  <!-- Gráfico -->
  {#if totalResults > 0}
    <div class="chart">
      <div class="diamond">
        <div class="style-point" style="left: {50 + results[0] * 10}%; top: {50}px;"></div>
        <div class="style-point" style="left: {50}px; top: {50 - results[1] * 10}%;"></div>
        <div class="style-point" style="left: {50 - results[2] * 10}%; top: {50}px;"></div>
        <div class="style-point" style="left: {50}px; top: {50 + results[3] * 10}%;"></div>
        <div class="line" style="left: 0; top: 50%; width: 100%;"></div>
        <div class="line" style="left: 50%; top: 0; height: 100%;"></div>
      </div>
    </div>
  {/if}
  
  <style>
    .column {
      display: inline-block;
      vertical-align: top;
      margin-right: 20px;
    }
  
    .row {
      margin-bottom: 5px;
    }
  
    .chart {
      margin-top: 20px;
      position: relative;
      width: 200px;
      height: 200px;
    }
  
    .diamond {
      position: absolute;
      width: 100%;
      height: 100%;
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
  