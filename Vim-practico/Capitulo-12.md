# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 12: Coincidencia de Patrones y Literales

Este capítulo explora cómo Vim interpreta los patrones de búsqueda. Aprenderás a controlar la sensibilidad a mayúsculas, a escribir búsquedas literales y expresiones regulares, y a delimitar coincidencias de manera precisa.

---

### Tip 73: Ajusta la Sensibilidad a Mayúsculas en Búsquedas

Opciones relevantes:

- `:set ignorecase` → ignora mayúsculas por defecto
- `:set smartcase`  → activa sensibilidad si hay alguna mayúscula en el patrón

Ejemplo:

    /foo      " Coincide con foo, Foo, FOO
    /Foo      " Solo coincide con Foo si smartcase está activado

---

### Tip 74: Usa el modificador `\v` para Expresiones Regulares

El modificador `\v` activa el modo "very magic", donde la mayoría de caracteres son especiales, facilitando expresiones compactas.

Ejemplo:

    /\v(abc|def)\d+    " Coincide con abc o def seguidos de uno o más dígitos

Sin `\v`, tendrías que escribirlo como:

    /\(abc\|def\)\d\

---

### Tip 75: Usa `\V` para Búsquedas Literales

`:\V` desactiva la interpretación de caracteres especiales.

Ejemplo:

    /\Vfoo.*bar    " Busca literalmente 'foo.*bar', no como una expresión regular

Ideal para buscar texto como rutas de archivos, URLs, o código sin preocuparte por escapar caracteres especiales.

---

### Tip 76: Usa Paréntesis para Capturar Subcoincidencias

Captura subgrupos dentro del patrón:

    /\v(foo)bar\1   " Coincide con 'foobarfoo'

También útil en sustituciones:

    :s/\v(foo)(bar)/\2\1/g   " Invierte 'foobar' a 'barfoo'

---

### Tip 77: Delimita los Límites de una Palabra

Usa `\<` y `\>` para definir límites de palabra:

    /\<word\>   " Coincide con la palabra exacta 'word'

Esto evita que 'password' o 'wording' coincidan.

---

### Tip 78: Delimita los Límites de una Coincidencia

Usa `\zs` para marcar dónde empieza la coincidencia y `\ze` dónde termina:

    /foo\zsbar   " Coincide solo con 'bar', dentro de 'foobar'

Permite reemplazar partes específicas de patrones complejos.

---

### Tip 79: Escapa Caracteres Problemáticos

Algunos caracteres tienen significados especiales en patrones (., *, +, etc.). Usa `\` para escaparlos.

Ejemplo:

    /foo\.bar    " Coincide con 'foo.bar', no 'foobar'

También puedes automatizar escapes en el registro de búsqueda:

    /\V<C-r>=escape(@u, getcmdtype().'\\')<CR>

Esto permite pegar texto literal desde un registro sin riesgo de errores de interpretación.

---

Este capítulo te equipa para escribir patrones de búsqueda potentes y seguros. Ya sea para búsquedas rápidas o sustituciones complejas, dominar estas técnicas te da un control quirúrgico sobre el texto.

