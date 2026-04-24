# Backward Path Studio

Aplicación web para editar grafos de forma visual y calcular el número de conjuntos independientes con un motor inspirado en el enfoque **backward path**. Incluye un lienzo interactivo, edición por nodos y aristas, exportación de casos y una sección de rendimiento con stress test.

## Descripción

Este proyecto es una mini app de una sola página que combina interfaz de usuario, lógica de grafos y visualización de rendimiento.  
El usuario puede pegar un grafo en texto, modificarlo visualmente y obtener métricas como `i(G)`, ancho estimado, tipo de caso detectado y tiempo de ejecución.

La interfaz soporta tema claro y oscuro mediante variables CSS, y la gráfica de rendimiento se genera con Chart.js.

## Características

- Editor visual de grafos con canvas.
- Modo mover nodos.
- Modo agregar nodo.
- Modo agregar arista.
- Modo eliminar nodo.
- Modo eliminar arista.
- Entrada textual compatible con formato de aristas `U V`.
- Cálculo automático del resultado al editar el grafo.
- Panel de stress test para medir tiempo contra tamaño de malla.
- Exportación de caso en TXT.
- Exportación de métricas en CSV.
- Casos guardados en memoria durante la sesión.
- Cambio de tema claro/oscuro.

## Interfaz

La app está organizada en dos zonas principales:

- Barra lateral izquierda: entrada de datos, herramientas de edición, controles de stress test y casos guardados.
- Área principal: resumen, canvas del grafo y panel de rendimiento.

## Estructura del proyecto

```text
index.html
```

Si prefieres separar archivos, la estructura recomendada sería:

```text
index.html
styles.css
app.js
```

## Requisitos

- Navegador moderno con soporte para `Canvas`, `Pointer Events` y `ES6+`.
- Conexión a Internet para cargar la fuente de Fontshare y Chart.js desde CDN.

## Uso

1. Abre el archivo HTML en el navegador.
2. Pega un grafo en el panel de entrada o usa el caso de ejemplo.
3. Usa el selector de modo para mover, agregar o eliminar nodos/aristas.
4. Presiona `Procesar` o `Calcular` para actualizar resultados.
5. Ejecuta el stress test para medir tiempos de cálculo en mallas cuadradas.

## Formato de entrada

El texto de entrada acepta una primera línea opcional con el número de nodos `N`.  
Después se listan aristas en formato `U V`, una por línea.

Ejemplo:

```txt
8
6 3
2 1
5 7
6 7
3 5
```

## Resultados mostrados

El panel de salida imprime información en este formato:

```txt
Cantidad de i(G): 55
Tiempo: 0.2000 ms
Caso detectado: camino simple
Ancho: 1
Componentes: 1
```

## Algoritmo

El motor `GraphEngine` implementa varios casos especiales antes de usar la estrategia general:

- Grafo vacío.
- Ciclo simple.
- Camino simple.
- Grafo desconectado.
- Caso general con búsqueda de camino Hamiltoniano aproximado y conteo con ventana backward path.

También incluye funciones auxiliares para detectar conectividad, obtener componentes, generar una ruta candidata y calcular el número total de conjuntos independientes según la estructura del grafo.

## Stress test

La sección de rendimiento genera mallas cuadradas `NxN`, calcula el resultado y grafica el tiempo de ejecución en una curva lineal con Chart.js.  
Esto permite comparar el comportamiento del algoritmo ante grafos cada vez más grandes.

## Exportación

- `Exportar CSV`: guarda métricas del grafo actual.
- `Descargar caso`: exporta el texto actual del grafo.
- `CSV stress`: descarga los resultados del stress test.

## Dependencias externas

- Chart.js para la gráfica de rendimiento.
- Fontshare Satoshi para la tipografía.

## Notas de implementación

- El tema visual se controla con `data-theme="light"` o `data-theme="dark"`.
- El canvas usa `touch-action: none` para mejorar interacción con Pointer Events.
- El gráfico de Chart.js se destruye antes de recrearse para evitar conflictos entre instancias.

## Posibles mejoras

- Separar el JavaScript en módulos.
- Guardar casos en `localStorage`.
- Añadir validación más estricta de entrada.
- Mostrar etiquetas o identificadores adicionales en el canvas.
- Exportar resultados del grafo en JSON además de CSV.

## Licencia

Uso académico y personal. Ajusta esta sección según la licencia que prefieras.
