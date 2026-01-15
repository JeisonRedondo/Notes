---
tags:
  - react
  - useContext
---
# useContext
Un context permite transmitir información desde el padre hacia otros componentes hijos, de forma nativa. Para desempeñar esta función se ah implementado un hook dentro de react llamado "useContext"

## Programación Reactiva
Se explica esta connotación aqui porque esta funcionalidad suele representar las basicas de la "Programación Reactiva".

Este hook representa un canal de comunicación el cual transmite información que permite que la pagina, basada en el diseño y demas reaccione alos cambios de los datos trasportados en este canal, eh de ahi el porque tenemos una explicación de la programación reactiva aqui.
## El provider
El provider es el gestionador que permite que se trasmita la información. Solo adentro de el es posible que se maneje el intercambio de información

## El prop del provider
Es aquel que contiene la información que se transmitira dentro del useContext con el provider, es un useState en el cual iremos agregando todo lo que necesitamos que se transmita en el context.

```js
    const App(){
        export const esteEsElContext = createContext({})

        const [estaEsLaDataDelContext,setEstaEsLaDataDelContext] = useContext("Aqui iria el valor por defecto")
        return(
            <esteEsElContext.provider value={{}}>
                //Aqui iran los hijos que deseamos que tengan acceso a la información almacenada dentro del context
            </esteEsElContext.provider>
            
        )

    }


```
