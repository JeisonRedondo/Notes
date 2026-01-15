---
tags:
  - react
  - vite
  - Introducción
---
## Trigger 
Es un evento, el cual va a iniciar un proceso de render. Este evento puede ser un botón, o un componente que cambia su estado interno. Existen dos tipos de trigger:
- Inicial : El que carga el componente inicial
- Re-render: Renderiza una vez, se hace un cambio y vuelve a renderizar.

## Dom - Dom Virtual

### DOM
 El DOM se refiere a la pagina que ay se ha cargado en el navegador, con ella react podrá comparar para verificar si hubo cambios.
### DOM - Virtual
El DOM - Virtual es la carga que obtiene react cuando se detecta que se han hecho cambios en los archivos, este se crea y luego se hace una comparación para verificar que ha cambiado con lo que ya se había cargado.

## Render
El render es por defecto la ejecución de una función la cuál usamos para crear el componente, al cargarse la función el contenido se carga en el DOM - Virtual el cual se compara con el DOM para poder entender donde ha cambiado la app.

## Commit en React 
Cuando react genera el proceso de comparación entre el DOM y el VirtualDOM, este define si debe o no aplicar cambios, en el caso de que se deba generar cambios, ese proceso en el cuál se hace el cambio es llamado un commit. Es en esencia aplicar el cambio y renderizarlo.