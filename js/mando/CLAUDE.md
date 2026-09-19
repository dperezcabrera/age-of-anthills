# mando/ — el catálogo del mando, COMPARTIDO por las dos interfaces

Aquí vive lo que decide **qué se puede mandar y cuándo**: `MENUS`, las insignias, los motivos,
las políticas de selección. Lo consumen `raton/` y `tablet/`.

- **Sin DOM y sin teclas.** Ni `document`, ni `innerHTML`, ni `shiftKey`. La prueba del bloque 04
  lo exige por texto y cargándolo en Node sin DOM. Si necesitas pintar o leer una tecla, eso va en
  la interfaz, y el catálogo recibe un **gesto** `{ sumar, todos, quitar }` o usa un enchufe
  (`conectar`, `conAvisos`, `alInvalidar`, `conPantallas`).
- **Cambiar aquí es cambiar las dos interfaces a la vez.** Un botón nuevo se añade aquí y las dos lo
  tienen; por eso se edita con la suite entera detrás y se dice en el commit.
- Lo que el catálogo necesita del motor llega por el paquete (`state`) y sale por los verbos
  (`net.*`). Si falta un dato, se pide al motor como cambio aparte; no se calcula aquí a medias.
