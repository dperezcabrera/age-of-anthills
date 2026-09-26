# tablet/ — la interfaz TÁCTIL (sin ratón ni teclado)

`input.js` son los dedos sobre el mapa: arrastrar mueve, toque elige, pulsación larga ordena (lo
que era el clic derecho), pinza hace zoom, doble toque centra. `ui.js` reexporta hoy el pintado del
ratón y añade lo que solo aquí hace falta (la ayuda por pulsación larga). `main.js` arranca con
`comun/arranque.js`, como el ratón. La página es `tablet.html` con `tablet.css` encima (44 px).

- **Qué hay bajo un punto y qué orden cae en una casilla NO se decide aquí**: es `mando/toque.js`,
  común con el ratón. Aquí solo se dice cómo se toca.
- **Los botones vienen del catálogo** (`mando/catalogo.js`) y reciben gestos, no teclas: si un gesto
  nuevo hace falta, se nombra en el catálogo y se produce aquí con un toque.
- Sin `title` que valga: todo consejo tiene que poder leerse con pulsación larga.
- Ver `DOS-UIS.md` (raíz) para lo que queda: mover el pintado a `comun/paneles.js`, el selector.
