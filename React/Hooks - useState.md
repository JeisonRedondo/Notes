---
tags:
  - react
  - useState
---
Un hook es un gancho, este nos permite generar una conexión con la detección de cambios. Con el hook useState accedemos a las características de react para detectar los cambios en esta asignación y poder re-renderizar el componente, así mostrándolo actualizado. 

## Batching
 El batching es una funcionalidad relacionada con la ejecución de varias asignaciones de hooks, los cuales modifican un mismo estado, esto podria generar problemas al ser ejecutados a la vez. Para controlar este tipo de eventos se implemento el batching, el cuál sirve para generar la carga de estas ejecuciones al final del proceso.  
