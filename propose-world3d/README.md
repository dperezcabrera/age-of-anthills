# El claro · prototipo de vista 3D

Propuesta visual independiente para Age of Anthills. Todo está dentro de esta carpeta. No modifica la vista actual, la simulación Rust/JS, las dependencias raíz ni el servidor.

## Abrir

Con el servidor habitual del juego abierto, visitar **`/propose-world3d/`**, por ejemplo `http://localhost:8080/propose-world3d/` si utiliza el puerto 8080. También puede servirse `public/` con cualquier servidor HTTP estático. No abrir `index.html` mediante `file://`: utiliza módulos ES.

Three.js 0.180.0 se incluye localmente con su licencia MIT. No requiere CDN, instalación npm ni conexión externa en ejecución. Requiere WebGL 2.

## Qué probar

1. Comparar **Valle → Ladera → Cresta**: el brote del otro lado pasa de oculto a visible.
2. Girar la cabeza: la zona azul responde al campo visual, no a la cámara.
3. Inclinar la mirada y activar **Solo lo que ve**.
4. Hacer clic sobre el terreno: la exploradora camina en línea recta apoyada en las alturas.
5. Arrastrar para orbitar y usar la rueda/pinza para zoom. Las flechas con el lienzo enfocado mueven la exploradora.

La casilla «Vida de la colonia» pausa el tránsito decorativo. Se inicia desactivada si se solicita movimiento reducido. No hay paseo de cámara automático. El diálogo de ayuda mantiene tamaño, scroll interno y controles visibles.

## Alcance y límites

- Terreno continuo con valle, ladera, cresta, meseta y montículo; es un escenario de autoría, **no el generador ni los niveles discretos del motor**.
- Una misma superficie triangulada se utiliza para dibujo, apoyo y oclusión. La cota indicada es altura de mundo, no un nivel entero del juego.
- Percepción de una observadora: origen simplificado a 0,38 unidades sobre su posición, pendiente × 0,35 más inclinación manual, campo horizontal 240°, vertical −65°/+35°, radio 16 y proximidad 1,1. Son parámetros de demostración, no una afirmación biológica.
- Oclusión mediante muestras cada 1/4 de casilla. No es la referencia exacta segmento/triángulo ni una implementación optimizada para miles de observadoras. Puede perder una arista muy fina. La máscara se actualiza como máximo a 10 Hz durante el movimiento.
- La máscara azul muestra suelo visible; el brote se prueba a una altura de 0,8. Un objetivo alto puede verse sin ver todo el suelo bajo él.
- «Solo lo que ve» oscurece el suelo no visible, omite decoración y filtra hormigas/brote. No hay memoria de exploración, niebla de colonia, información de servidor ni protección antitrampas.
- 49 hormigas de demostración con cuerpos y apéndices instanciados; las acompañantes siguen un circuito, sin IA, A*, colisión o trabajo real. El anillo de selección se dibuja por encima para conservar legibilidad.
- Las piedras, agua y plantas son decoración; no ocluyen ni bloquean el movimiento. El montículo del nido sí pertenece al terreno.
- Una luz con sombras, vegetación instanciada, materiales simples, sin postprocesado pesado. No es un benchmark de rendimiento ni un acabado AAA terminado.

## Archivos y comprobaciones

- `terrain.js`: superficie y percepción, sin dependencia gráfica.
- `landscape.js`: representación gráfica del paisaje.
- `colony.js`: geometría e instancias de hormigas.
- `main.js`: escena, cámara, controles y reloj del prototipo.
- `terrain.test.js`: regresiones geométricas. Ejecutar `node --test public/propose-world3d/terrain.test.js` desde la raíz.

Esta separación mantiene las decisiones de superficie independientes del formato de Three.js, sin introducir una capa genérica de motores gráficos.

Referencias: [instalación oficial de Three.js](https://threejs.org/manual/en/installation.html), [mallas instanciadas](https://threejs.org/docs/pages/InstancedMesh.html). La propuesta de arquitectura completa está en `ux/propuesta-vista-aaa-y-vision-multinivel.md`.
