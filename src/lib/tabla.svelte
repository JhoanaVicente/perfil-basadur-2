<script>
    let results = [0, 0, 0, 0]; // Inicializa los resultados de las cuatro columnas
    const excludedRows = new Set([1, 2, 5, 10, 14, 17]); // Define las filas que se excluyen del cálculo
    let totalResults = 0; // Variable para almacenar el total de resultados
  
    // Matriz de palabras para cada fila
    const words = [
      ["Alerta", "Equilibrada", "Lista", "Ansiosa"],
      ["Paciente", "Atenta", "Contundente", "Preparada"],
      ["Hacer", "Infantil", "Observar", "Realista"],
      ["Experimentar", "Diversificar", "Esperar", "Consolidar"],
      ["Reservada", "Seria", "Gozador", "Juguetona"],
      ["Ensayo y Error", "Alternativas", "Sopesar", "Evaluar"],
      ["Actuar", "Divergir", "Abstraer", "Convergir"],
      ["Directa", "Posibilidades", "Conceptual", "Realidades"],
      ["Implicada", "Cambiar Perspectivas", "Teórico", "Enfocar"],
      ["Silenciosa", "Confiable", "Responsable", "Imaginativa"],
      ["Implementar", "Visualizar", "Describir", "Seleccionar"],
      ["Ejecutar", "Orientado al futuro", "Leer", "Detallista"],
      ["Física", "Crear opciones", "Mental", "Decidir"],
      ["Impersonal", "Orgullosa", "Esperanzada", "Temeroso"],
      ["Practicar", "Transformar", "Pensar", "Elegir"],
      ["Manejar", "Especular", "Contemplar", "Juzgar"],
      ["Simpatizar", "Práctica", "Emotiva", "Demorar"],
      ["Tomar contacto", "Diferenciar", "Reflexionar", "Asegurar"]
    ];
  
    function handleChange(columnIndex, rowIndex, value) {
      // Verifica si la fila actual está en la lista de filas excluidas
      if (!excludedRows.has(rowIndex + 1)) {
        results[columnIndex] = 0; // Restablece el resultado de la columna
        // Recalcula el resultado de la columna sumando todas las opciones seleccionadas
        for (let i = 0; i < words.length; i++) {
          if (!excludedRows.has(i + 1)) { // Asegura que las filas excluidas no se sumen al total
            results[columnIndex] += +document.getElementById(`select-${columnIndex}-${i}`).value;
          }
        }
      }
      // Calcula el total de resultados
      totalResults = results.reduce((acc, columnTotal) => acc + columnTotal, 0);
    }
  </script>
  
  {#each [0, 1, 2, 3] as columnIndex}
    <div class="column">
      <h2>Columna {columnIndex + 1}</h2>
      {#each words as wordSet, rowIndex}
        <div class="row">
          <span>{wordSet[columnIndex]}</span>
          <select id={`select-${columnIndex}-${rowIndex}`} on:change={(event) => handleChange(columnIndex, rowIndex, +event.target.value)}>
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
        <div class="style-point" style="left: {50 + results[0]}%; top: {50}%;"></div>
        <div class="style-point" style="left: {50}%; top: {50 - results[1]}%;"></div>
        <div class="style-point" style="left: {50 - results[2]}%; top: {50}%;"></div>
        <div class="style-point" style="left: {50}%; top: {50 + results[3]}%;"></div>
        <svg style="position: absolute; width: 100%; height: 100%;">
          <line x1="{50 + results[0]}%" y1="{50}%" x2="{50}%" y2="{50 - results[1]}%" style="stroke:blue;stroke-width:2" />
          <line x1="{50}%" y1="{50 - results[1]}%" x2="{50 - results[2]}%" y2="{50}%" style="stroke:blue;stroke-width:2" />
          <line x1="{50 - results[2]}%" y1="{50}%" x2="{50}%" y2="{50 + results[3]}%" style="stroke:blue;stroke-width:2" />
          <line x1="{50}%" y1="{50 + results[3]}%" x2="{50 + results[0]}%" y2="{50}%" style="stroke:blue;stroke-width:2" />
        </svg>
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
  
    .column {
        margin: 28px 28px ;
    }
  
    .row {
        display: flex;
        text-align: center;
        justify-content: space-between;
        font-size: medium;
    }
  </style>
  