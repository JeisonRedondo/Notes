---
tags:
  - vite
  - react
  - typescript
---
### Conceptos Básicos
##### StrictMode
El strict mode se usa para comprobar que realmente se estan cargando componentes dentro del bundle de react, en concreto el componente se crea se destruye, se verifica que de estas partes luego al volver a montarlas sea el mismo componente, y luego se vuelve a crear.

##### Single Page Application
Hablamos de una SPA cuando tenemos en una sola pagina toda una aplicación, esto por que en este lugar tenemos anclada la carga de la aplicación que iremos actualizando dado sea necesario.
#### React-Dom
##### CreateRoot
Este método crea la base donde se cargara la todo el contenido de la pagina.