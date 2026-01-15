# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 14: Sustitución

Este capítulo revela que el comando `:substitute` (`:s`) no es solo para búsquedas simples, sino una de las herramientas más poderosas de Vim para manipular texto.

---

### Tip 88: Conoce el Comando Substitute

El comando:

    :[rango]s/{patrón}/{reemplazo}/[flags]

Donde:
- `[rango]` especifica líneas donde aplicar la sustitución.
- `{patrón}` es la expresión regular.
- `{reemplazo}` es el texto sustitutivo.
- `[flags]` modifican el comportamiento.

Flags útiles:
- `g` – sustituye todas las coincidencias en la línea.
- `c` – confirma cada sustitución.
- `n` – muestra cuántas ocurrencias habría, sin cambiar texto.
- `e` – evita error si no hay coincidencias.

---

### Tip 89: Busca y Sustituye Todas las Coincidencias

Por defecto `:s` actúa sobre la línea actual y solo cambia la primera coincidencia. Para cambiar todo:

    :%s/antiguo/nuevo/g

`%` indica todas las líneas, y `g` aplica globalmente en cada línea.

---

### Tip 90: Revisa Cada Sustitución Manualmente

Usa la flag `c` para confirmar cada cambio:

    :%s/contenido/copia/gc

Responde:
- `y` – sí
- `n` – no
- `a` – todas
- `q` – cancelar
- `l` – solo esta y salir
- `<C-e>` / `<C-y>` – mover pantalla

Ideal para casos ambiguos como homónimos o heterónimos.

---

### Tip 91: Reutiliza el Último Patrón de Búsqueda

Puedes dejar en blanco el campo de búsqueda para reutilizar el último patrón:

    /patrón
    :%s//reemplazo/g

Esto separa búsqueda y sustitución, permitiendo probar patrones sin alterar el buffer.

---

### Tip 92: Sustituye con el Contenido de un Registro

Para insertar texto previamente copiado (por ejemplo desde el registro 0):

    :%s//\=@0/g

Evalúa el contenido del registro y lo usa como reemplazo.

---

### Tip 93: Repite el Último Comando Substitute

Repite la sustitución anterior con los mismos parámetros:

    :&&

También puedes usar `&` como flag para repetir flags previos.

---

### Tip 94: Reorganiza Campos CSV con Subcoincidencias

Usa `\1`, `\2`, etc., para referirse a grupos capturados:

    :%s/\([^,]*\),\([^,]*\)/\2,\1/

Intercambia dos columnas separadas por coma.

---

### Tip 95: Realiza Operaciones Aritméticas en el Reemplazo

Aplica aritmética usando `\=` y `submatch()`:

    :%s//\=submatch(0)+1/g

Reemplaza números coincidentes incrementándolos.

---

### Tip 96: Intercambia Dos o Más Palabras

Con diccionarios Vim script:

    :%s/\v(dog|man)/\={'dog':'man','man':'dog'}[submatch(0)]/g

Intercambia "dog" y "man" (y viceversa) de forma segura.

---

### Tip 97: Sustituye en Varios Archivos

Usa `:argdo` para aplicar sustituciones a múltiples archivos:

    :args *.txt
    :argdo %s/Pragmatic/Practical/gc | update

Revisa cada uno con confirmación (`c`) y guarda con `update`.

---

Este capítulo te brinda dominio del comando `:substitute`, desde los usos más comunes hasta combinaciones con expresiones regulares, registros, aritmética y manipulación en múltiples archivos. Una herramienta esencial para editar texto a escala.

