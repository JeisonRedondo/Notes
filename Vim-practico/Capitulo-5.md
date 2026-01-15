# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 5: Modo Línea de Comandos

Vim hereda mucho de sus ancestros Unix: `ed`, `ex` y `vi`. El modo Línea de Comandos es uno de los vestigios más potentes de ese linaje. Aunque muchas tareas pueden hacerse desde el modo Normal, los comandos Ex ofrecen una forma poderosa de trabajar con múltiples líneas de texto a la vez.

---

### Tip 27: Conoce la Línea de Comandos de Vim

Cuando presionamos `:` entramos al modo Línea de Comandos. Aquí podemos ejecutar comandos Ex, patrones de búsqueda o expresiones.

Algunos comandos útiles:

| Acción                                | Comando           |
|---------------------------------------|-------------------|
| Borrar líneas                         | `:[rango]delete`  |
| Copiar líneas                         | `:[rango]yank`    |
| Pegar líneas                          | `:[línea]put`     |

Otros accesos al modo Línea de Comandos incluyen `/` para buscar y `<C-r>=` para evaluaciones.

---

### Tip 28: Ejecutar un Comando en Múltiples Líneas Consecutivas

Los comandos Ex aceptan rangos. Puedes especificar rangos de varias maneras:

    :2,5p      " imprimir líneas 2 a 5
    :1,$d      " eliminar desde la línea 1 hasta el final
    :.,+3s/foo/bar/  " sustituye en línea actual y las 3 siguientes

Incluso puedes usar patrones:

    :/Inicio/,/Fin/d    " borrar entre líneas que contienen 'Inicio' y 'Fin'

---

### Tip 29: Duplicar o Mover Líneas con :t y :m

Comandos para duplicar (`:t`) o mover (`:m`) líneas:

| Acción                              | Comando     |
|-------------------------------------|-------------|
| Copiar línea actual bajo línea 6    | `:.t6`      |
| Mover línea actual al inicio        | `:.m0`      |
| Copiar selección visual al final    | `'<,'>t$`   |

Ejemplo práctico:

    :6t.   " copia la línea 6 bajo la actual
    :2,4m$ " mueve líneas 2-4 al final

---

### Tip 30: Ejecutar Comandos del Modo Normal en un Rango

Usa `:normal` para aplicar comandos como si los escribieras en modo Normal:

    :2,5normal A;     " añade ';' al final de líneas 2 a 5

Puedes combinarlo con `g`:

    :g/patron/normal ^i//   " añade '//' al inicio de líneas que contienen 'patron'

---

### Tip 31: Repetir el Último Comando Ex

Con `@:` repites el último comando Ex. También puedes usar:

    :↑      " flecha arriba para recuperar
    q:      " ventana de historial de comandos

---

### Tip 32: Autocompleta tus Comandos Ex

Presiona `<Tab>` mientras escribes un comando para autocompletarlo. Funciona con:

- Nombres de comandos (`:w`, `:s`, etc.)
- Archivos (`:e f<Tab>`)
- Opciones (`:set n<Tab>`)

También puedes usar `<C-d>` para ver una lista de coincidencias.

---

### Tip 33: Inserta la Palabra Actual en el Prompt

En la línea de comandos, puedes insertar:

| Acción                                | Comando         |
|---------------------------------------|-----------------|
| Palabra bajo el cursor                | `<C-r><C-w>`    |
| WORD (sin espacios) bajo el cursor    | `<C-r><C-a>`    |

Ejemplo:

    :s/foo/<C-r><C-w>/g   " sustituye por la palabra actual

---

### Tip 34: Recupera Comandos del Historial

Presiona:

- `↑` y `↓` para recorrer comandos anteriores.
- `q:` para abrir la ventana de historial y editarlos como en un buffer.

Puedes navegar, buscar (`/`) y ejecutar (`<CR>`).

---

### Tip 35: Ejecuta Comandos en la Terminal

Puedes ejecutar comandos de shell directamente:

    :!ls         " lista archivos
    :!make       " compila
    :!ruby %     " ejecuta archivo actual con Ruby

También puedes combinarlos:

    :w | !ruby %   " guarda y ejecuta

---

### Tip 36: Ejecuta Varios Comandos Ex en Secuencia

Usa `|` para encadenar:

    :g/foo/d | %s/bar/baz/g | update

Ejecuta varios comandos seguidos. Ideal para macros o scripts de edición.

---
