# raton/ — la interfaz de RATÓN Y TECLADO

`ui.js` construye y refresca los paneles, la tira de hormigueros y la de tipos, las pantallas
(configurar, salas, final), los avisos y el foco del mando; `input.js` son los gestos del ratón y
las teclas sobre el mapa; `main.js` arranca el cliente y atiende los paquetes.

- **Aquí se pinta y se pulsa; aquí NO se decide qué se puede mandar.** Eso está en
  `../mando/catalogo.js`, y `ui.js` lo reexporta para que las pruebas sigan importando de aquí.
- **Las teclas se traducen en UN sitio**: `gestoDe(ev)` en `ui.js` (Mayús = todos, Ctrl/Cmd/Mayús =
  sumar, clic derecho = quitar). Un botón nuevo que necesite un modificador se expresa como gesto,
  no como tecla, para que la tablet lo tenga.
- El dibujo del mapa (`../view.js`, `../skins/`) es común a las dos interfaces: aquí solo se le
  pasa el estado.
- Ver `DOS-UIS.md` en la raíz: los pasos que faltan (handlers comunes, `tablet/`).
