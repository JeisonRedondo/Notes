# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 13: Búsqueda

Después de estudiar el motor de expresiones regulares de Vim en el capítulo anterior, ahora veremos cómo aprovecharlo con el comando de búsqueda. Este capítulo cubre desde búsquedas básicas hasta técnicas avanzadas para navegar y trabajar con coincidencias encontradas.

---

### Tip 80: Conoce el Comando de Búsqueda

Desde el modo Normal:

    /texto<CR>     " Busca hacia adelante
    ?texto<CR>     " Busca hacia atrás

Repite la última búsqueda:

    n              " Siguiente coincidencia
    N              " Coincidencia anterior

Presionar `<Esc>` cancela la búsqueda. Puedes navegar el historial con las flechas o `<C-f>`.

---

### Tip 81: Resalta las Coincidencias

Activa el resaltado automático:

    :set hlsearch

Para desactivarlo:

    :set nohlsearch

Usa `:nohlsearch` para limpiar el resaltado tras una búsqueda.

Para activar la búsqueda incremental (ver mientras escribes):

    :set incsearch

---

### Tip 82: Previsualiza la Primera Coincidencia Antes de Ejecutar

Gracias a `incsearch`, puedes ver dónde caerá el cursor sin presionar `<CR>` aún. Esto te da retroalimentación inmediata al escribir el patrón.

Ideal para evitar errores en búsquedas largas o complejas.

---

### Tip 83: Mueve el Cursor al Final de la Coincidencia

Usa un desplazamiento:

    /vim/e<CR>   " Mueve el cursor al final de la coincidencia

Otros sufijos útiles:

| Sufijo | Descripción                    |
|--------|--------------------------------|
| /e     | Fin del patrón                 |
| /s     | Inicio del patrón              |
| /+n    | n líneas después del patrón    |
| /-n    | n líneas antes del patrón      |

---

### Tip 84: Opera en Toda la Coincidencia

Usa los modificadores `\zs` y `\ze` para delimitar la coincidencia exacta sobre la que operar.

Ejemplo:

    :s/\vstart\zs.*\zeend/reemplazo/g

Esto sustituye solo el contenido entre "start" y "end".

---

### Tip 85: Crea Patrones Complejos Iterando desde el Historial

Vuelve al último patrón de búsqueda con:

    /<Up>    " Historial de patrones

O bien:

    q/       " Abre el historial en una ventana editable
    <CR>     " Ejecuta la búsqueda

Ideal para depurar expresiones regulares complejas.

---

### Tip 86: Cuenta las Coincidencias del Patrón Actual

Usa este comando:

    :%s/patrón//gn

Esto no sustituye nada, pero imprime cuántas veces aparece el patrón.

---

### Tip 87: Busca la Selección Visual Actual

Sobrescribe `*` para que funcione en modo visual:

```vim
vnoremap * y/\V<C-R>=escape(@", '/')<CR><CR>

Esto copia la selección y realiza una búsqueda literal escapada automáticamente.

Este capítulo te da las herramientas para usar búsquedas en Vim no solo como navegación, sino como una poderosa extensión de edición de texto guiada por patrones.



