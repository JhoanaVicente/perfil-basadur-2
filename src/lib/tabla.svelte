<script>
    let respuestas = [
      [4, 3, 2, 1], // Fila 1
      [1, 2, 3, 4], // Fila 2
      // Continuar con las 16 filas restantes
    ];
    let resultados = [0, 0, 0, 0]; // Array para almacenar los resultados de las columnas
  
    // Función para calcular los resultados
    function calcularResultados() {
      resultados = [0, 0, 0, 0]; // Reinicia los resultados
  
      // Suma las respuestas por columnas
      respuestas.forEach((fila) => {
        fila.forEach((respuesta, index) => {
          // @ts-ignore
          resultados[index] += parseInt(respuesta);
        });
      });
  
      // Verifica si la suma total es igual a 240
      if (resultados.reduce((a, b) => a + b, 0) === 240) {
        console.log("Resultados:", resultados);
      } else {
        console.error("La suma total no es igual a 240. Por favor, revisa tus respuestas.");
      }
    }
  </script>
  
  <style>
    /* Estilos opcionales para la apariencia */
    table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 20px;
    }
  
    th, td {
      border: 1px solid black;
      padding: 8px;
      text-align: center;
    }
  </style>
  
  <section>
    <h1>Test de Personalidad</h1>
    <table>
      <thead>
        <tr>
          <th></th>
          <th>Columna 1</th>
          <th>Columna 2</th>
          <th>Columna 3</th>
          <th>Columna 4</th>
        </tr>
      </thead>
      <tbody>
        {#each respuestas as fila, i}
          <tr>
            <td>Fila {i + 1}</td>
            {#each fila as respuesta, j}
              <td>
                <input type="radio" bind:group={respuestas[i][j]} value="4">
                <input type="radio" bind:group={respuestas[i][j]} value="3">
                <input type="radio" bind:group={respuestas[i][j]} value="2">
                <input type="radio" bind:group={respuestas[i][j]} value="1">
              </td>
            {/each}
          </tr>
        {/each}
      </tbody>
    </table>
    <button on:click={calcularResultados}>Calcular Resultado</button>
  </section>
  