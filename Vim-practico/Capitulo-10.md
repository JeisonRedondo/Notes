# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 10: Copiar y Pegar

En Vim, las operaciones de cortar, copiar y pegar no se manejan con un solo portapapeles global, sino a través de múltiples registros. Este capítulo explora cómo aprovechar los comandos `delete`, `yank`, `put` y cómo interactuar con el portapapeles del sistema.

---

### Tip 60: Elimina, Copia y Pega con el Registro No Nombrado

Los comandos:

    d      → delete (corta)
    y      → yank (copia)
    p      → put (pega)

Vim utiliza un registro "no nombrado" automáticamente. Si usas `x` o `dd`, el texto se guarda en este registro. Luego puedes pegar con `p` o `P`.

Ejemplo: transponer caracteres

    Texto inicial: Practica lvim
    Comandos: F␣ x p
    Resultado: Practical vim

Ejemplo: transponer líneas

    dd     → corta línea
    p      → la pega debajo

---

### Tip 61: Comprende los Registros de Vim

Vim tiene varios registros:

| Registro         | Contenido                                |
|------------------|-------------------------------------------|
| "                | Registro no nombrado                      |
| "0               | Última copia (yank)                       |
| "1 - "9          | Historial de eliminaciones                |
| ":               | Último comando Ex                         |
| "/               | Último patrón de búsqueda                 |
| "+ / "*          | Portapapeles del sistema (requiere soporte) |

Comando para ver los registros:

    :registers

Puedes especificar un registro usando comillas dobles:

    "0p     → pega lo último copiado
    "2p     → pega el segundo elemento borrado
    "+y     → copia al portapapeles del sistema
    "+p     → pega desde el portapapeles del sistema

---

### Tip 62: Reemplaza una Selección Visual con un Registro

Cuando seleccionas texto en modo Visual y luego presionas `p`, Vim reemplaza la selección con el contenido del registro no nombrado y guarda la selección sobrescrita en ese mismo registro.

Esto puede llevar a resultados inesperados si presionas `u` (undo) y luego `gv` (reselect) seguido de `p`.

Solución:

    "0p     → asegura que pegues lo que copiaste antes

Este comportamiento permite técnicas como:

**Intercambiar palabras**

    I like chips and fish.
    Acción: elimina "chips", mueve cursor a "fish", p

Resultado: I like fish and chips.

---

### Tip 63: Pega desde un Registro

Comandos para pegar desde registros específicos:

    "ayy     → copia línea en registro `a`
    "ap      → pega contenido del registro `a`

Ejemplo de uso en macros, múltiples yanks, o reutilización de contenidos intermedios.

---

### Tip 64: Interactúa con el Portapapeles del Sistema

Cuando Vim tiene soporte de `+clipboard`, puedes usar:

    "+y     → copiar al portapapeles
    "+p     → pegar desde el portapapeles

Esto permite interoperar con el sistema operativo, navegadores, IDEs, etc.

Comprobar soporte:

    vim --version | grep clipboard

Busca `+clipboard` o `+xterm_clipboard`.

Si no tienes soporte, considera instalar `gvim`, o recompilar Vim con `--with-features=huge`.

---

Este capítulo te equipa con técnicas poderosas para manipular texto usando registros. Desde operaciones simples hasta macros complejas, dominar los registros te permite trabajar con texto a una velocidad sorprendente.
