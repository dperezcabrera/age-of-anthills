# Guía de campo

Módulo autocontenido de ayuda para Age of Anthills. Organiza 35 fichas sobre especies, hormigas, la construcción del hormiguero, el mundo y los bichos del campo como una pequeña wiki en español e inglés.

La portada es un índice compacto. Cada sección tiene su propia página y cada ficha se abre de forma aislada, con migas de navegación, enlaces relacionados y URL compartible. Las cinco especies jugables incluyen además una referencia natural con fotografía, curiosidades y fuentes.

## Abrir la página independiente

Con el servidor del juego en marcha:

```text
http://localhost:8080/guide/
```

La guía se publica únicamente bajo `/guide/`.

Las fichas aceptan enlaces profundos:

```text
/guide/#especies/cortadora
/guide/#caracteristicas/rasgos
/guide/#hormiguero/fundacion
/guide/#mundo/marabunta
/guide/#fauna/saltamontes
```

También se puede enlazar al índice de una sección:

```text
/guide/#especies
/guide/#caracteristicas
/guide/#hormiguero
/guide/#mundo
/guide/#fauna
```

## API de integración

`index.js` expone una sola operación de montaje. El objeto resultante permite abrir una ficha y destruir la instancia:

```js
import { montarGuia } from '../guide/index.js';

const guia = montarGuia(contenedor, { idioma: 'es' });
guia.abrir('especies', 'especies/cortadora');
guia.destruir();
```

Para integrarla en el juego, el llamador debe:

1. Cargar `guia.css`.
2. Proporcionar el cuerpo de un `<dialog>` nativo como contenedor.
3. Abrir el diálogo y devolver el foco al botón que lo lanzó al cerrar.

La guía no conoce el overlay, el estado global ni la implementación del panel de control.

## Fuentes de verdad

- Los textos explicativos viven en `especies.js`, `caracteristicas.js`, `hormiguero.js`, `mundo.js` y `fauna.js`.
- Las referencias biológicas y los créditos de las imágenes viven en `naturaleza.js`.
- Los modificadores numéricos de especie se obtienen mediante `resolverEspecie` desde el motor.
- La carne, la vida, el paso y el peso del brote de cada bicho se LEEN de `sim/fauna.js` y se pasan a unidades de pantalla con `sim/comida.js`: la sección «Los bichos» no copia ni un número del catálogo. Lo único escrito a mano ahí es la prosa y el coste MEDIDO de cazar cada pieza, que lleva su protocolo y su fecha en la cabecera de `fauna.js`.
- `catalogo.js` oculta localización, búsqueda, orden y resolución de enlaces relacionados.
- Las fichas entregan texto estructurado a la vista; no contienen HTML ejecutable.

## Fotografías y fuentes externas

Las fotografías se cargan desde `upload.wikimedia.org`, con dimensiones reservadas para evitar saltos de layout. Cada imagen muestra un enlace a su página de archivo en Wikimedia Commons, autoría y licencia; la explicación biológica enlaza a la página correspondiente de Wikipedia.

La guía sigue funcionando si una imagen externa no está disponible: conserva el espacio y muestra el texto alternativo. El contenido del juego y la navegación no dependen de la respuesta de Wikimedia.

## Verificación

```sh
node test.js guide      # cableada en la suite: si la guía se pudre, la suite se pone roja
```

La prueba comprueba los dos idiomas —y que estén TRADUCIDOS de verdad, no repetidos—, identidades
únicas, reparto por secciones, contenido mínimo, SVG, enlaces relacionados que RESUELVEN (una
relación a una ficha inexistente se caía en silencio), búsqueda sin acentos, metadatos de las cinco
referencias naturales, los créditos del sonido, que ninguna ficha de especie prometa una casta que
el mando no deja reclutar y que el bestiario tenga UNA ficha por pieza del catálogo de fauna —ni una
de más— con la carne y la vida que dice el motor.
