---
tags:
  - useEffect
  - react
---

## useEffect
Es un hook que según la wiki permite tener control del ciclo de vida de un componente, sin embargo según nuestro profe gentleman, es aconsejable tener mas en cuenta su uso para cuando necesitamos hacer una sincronización con entidades externas como llamados a APIS.
## Cuando se ejecuta el useEffect
El useEffect se ejecuta cuando se genera un render en el componente
### Cuando?
- Cuando se monta el componente
- Cada vez que se modifique el valor de los states, los cuales están relacionados con el useEffect  a través del arreglo de dependencias.
### Se puede usar mas de una vez useEffec
Si, normalmente querremos en algunos proyectos ejecutar cierta logica dependiendo de las variaciones de ciertos parametros, es en estas ocasiones cuando podriamos usar mas de un useEffect.
## Arreglo de dependencias
Cuandos definimos por defecto el useEffect este nos proporciona al fina de la arrow function, un arreglo. En este arreglo([]) debemos poner aquellos estados de los cuales necesita estar consciente el Effect para actualizarse, así podra presentar la información de la manera adecuada.
### Y si no pongo el arreglo de dependecias?
Entonces el Effect se actualizara cada vez que se actualice un estado dentro del componente generando una carga extra en la carga de la aplicación.

## return
El return dentro de useEffect es un metodo, este solo se ejecutara cuando el componente se destruya, muera, es entonces cuando este return ejecutara su contenido.
### Porque fue diseñado así?
La idea detras de este diseño es poder manejar los estados de la memoria como principal objetivo, y también ejercer algunas tareas de desconexión en la misma.