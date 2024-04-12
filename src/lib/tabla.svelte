<script>
    let results = [0, 0, 0, 0]; // Inicializa los resultados de las cuatro columnas
    const excludedRows = new Set([1, 2, 5, 10, 14, 17]); // Define las filas que se excluyen del cálculo
  
    function handleChange(columnIndex, rowIndex, value) {
      // Verifica si la fila actual está en la lista de filas excluidas
      if (!excludedRows.has(rowIndex + 1)) {
        results[columnIndex] += value; // Actualiza el resultado de la columna
      }
    }
  
    function getTotalResult() {
      return results.reduce((acc, columnTotal) => acc + columnTotal, 0); // Suma los resultados de todas las columnas
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
  
  <h2>Total: {getTotalResult()}</h2>
  
  <style>
    .column {
      display: inline-block;
      vertical-align: top;
      margin-right: 20px;
    }
  
    .row {
      margin-bottom: 5px;
    }
  </style>
  