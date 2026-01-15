# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 9: Navegar Entre Archivos con Saltos

Mientras que los movimientos (`motions`) nos permiten movernos dentro de un archivo, los *saltos* (`jumps`) nos permiten navegar entre ubicaciones, incluso entre archivos distintos. Este capítulo explora cómo Vim rastrea tu camino y te permite volver atrás fácilmente.

---

### Tip 56: Recorre la Lista de Saltos

Vim mantiene una lista de saltos para recordar de dónde vienes y hacia dónde vas.

    <C-o>   " Ir atrás en la lista de saltos
    <C-i>   " Ir adelante (como un 'adelante' en navegador)

También puedes ver la lista de saltos:

    :jumps

Ejemplos de acciones que generan un salto:

| Acción                              | Comando        |
|-------------------------------------|----------------|
| Ir a una línea específica           | `[n]G`         |
| Buscar patrón                       | `/pattern`     |
| Saltar entre paréntesis emparejados| `%`            |
| Ir al principio de párrafo/sentencia| `{` / `(`      |
| Saltar a nombre de archivo          | `gf`           |
| Saltar a definición (tag)           | `<C-]>`        |
| Saltar a una marca                  | `'a` o `` `a ``|

---

### Tip 57: Recorre la Lista de Cambios

Vim también rastrea los lugares donde hiciste ediciones. Puedes moverte entre ellos usando:

    g;   " Anterior cambio
    g,   " Siguiente cambio

Útil para revisar cambios recientes en un archivo largo sin perder el contexto.

---

### Tip 58: Salta al Nombre de Archivo Bajo el Cursor

Cuando el cursor está sobre una ruta o nombre de archivo, puedes abrirlo:

    gf     " Abre el archivo bajo el cursor

Asegúrate de que la opción `'path'` esté configurada adecuadamente, por ejemplo:

    :set path+=**

Y para ayudar con extensiones:

    :set suffixesadd=.js,.ts,.jsx,.ts,.html,.css

Si el archivo está en un directorio relativo al actual, funcionará directamente.

---

### Tip 59: Salta Entre Archivos Usando Marcas Globales

Puedes usar marcas con letras mayúsculas para establecer posiciones entre archivos:

    mA     " Establecer marca global 'A'
    'A     " Volver a esa ubicación (línea de inicio)
    `A     " Volver a esa ubicación (columna exacta)

Las marcas A-Z se mantienen incluso cuando cambias de archivo, a diferencia de las a-z que son locales.
