---
tags:
- typescript
- introducción
---

## Typescript
- Implementa tipos para javascript, con el fin de evitar errores de tipado
- Ayuda a generar codigo mas limpio al describir explicitamente lo que se pretende obtener o recibir,
evitando tener que describir esto en la semantica.
- Al ser de tipo estatico el código se evalua antes de ser ejecutado.

## Las basícas
- **Emisión con errores**: La emisión con errores ah demostrado ser espectacular para evitar errores recurrentes en js,
si el programador no desea tenerla activa la puede apagar con "tsc --noEmitOnError file.ts"
- **Tipos Explicitos**: Los casos donde necesitamos tener un tipado depende de cuando deba de ser aclarado explicitamente,
pues ts tiene uan herramienta que tipa por defecto la mayoria de las variables y demas, haciendo del tipado algo opcional.
- **Tipado borrado**: ts por lo general no se puede ejecutar en los navegadores, por ello se necesita un compilador que traduzca
el ts a js para que así pueda ser intrepretado por el navegador.
- **Versionado Antiguo**:Cuando se ejecuta el compilador de ts, este por defecto interpreta el código y luego usa una versión antigua de js para reescribirlo, esto con el fin de evitar inconvenientes de versiones no compatibles con las versiones de navegadores.
- **Modo Estricto**: El modo estricto así como se puede desactivar tambien se puede bajar o subir controlando su intensidad.
- **noImplicityAny**: Al llamarlo ts no intentara inferir los tipos, dejando esta parte del código desatendida de la verificación,
pero esto haria perder el sentido de trabajar con ts, por ende no es recomendado.
- **strictNullchecks**:Nos hace mas evidente el uso de este tipo de valores, pues por lo general esto puede muchas veces 
hacernos recaer en errores.
