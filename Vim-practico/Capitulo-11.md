# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 11: Macros

Las macros en Vim permiten grabar secuencias de comandos para repetir acciones. Aunque el comando punto (`.`) es útil para repetir cambios simples, las macros permiten automatizar tareas más complejas o repetitivas sobre múltiples líneas, bloques o archivos.

---

### Tip 65: Graba y Ejecuta una Macro

Usa la tecla `q` seguida de una letra de registro (como `q`, `a`, `b`, etc.) para comenzar a grabar:

    qq       " Comienza grabación en el registro 'q'
    ...      " Ejecuta comandos
    q        " Finaliza grabación

Para ejecutar la macro grabada:

    @q       " Ejecuta la macro del registro q
    @@       " Repite la última macro ejecutada

Ejemplo de grabación y ejecución:

    qa       " Graba en el registro 'a'
    I• <Esc> " Inserta punto en cada línea
    j        " Baja una línea
    q        " Termina grabación

    5@a      " Ejecuta la macro 5 veces

---

### Tip 66: Normaliza, Apunta, Aborta

Cuando grabes macros:

- **Normaliza** la posición del cursor al inicio (usa `0`, `gg`, etc.)
- Usa movimientos repetibles como `w`, `e`, `0`, no `l`, `h`
- Aborta con `:undo` o `q!` si cometes errores

Ejemplo:

    0e       " Salta al final de la primera palabra
    ciwTexto<Esc> " Cambia palabra de forma segura

Así garantizas que la macro funcione de forma consistente en múltiples contextos.

---

### Tip 67: Reproduce con un Contador

Aunque `;.` es útil para repetir acciones, no admite repetición con conteo. Una macro puede lograrlo:

    qq;.q    " Graba la secuencia ;. en 'q'
    11@q     " Ejecuta 11 veces

Esto simula `11;.` con gran precisión, útil en refactorizaciones en masa.

---

### Tip 68: Repite un Cambio en Líneas Contiguas

Para aplicar una macro a líneas contiguas:

    qaComandosq   " Graba macro
    5@a           " Ejecuta 5 veces en serie

También puedes usar selección visual y:

    :'<,'>normal @a

Esto ejecuta la macro sobre cada línea seleccionada de forma *paralela*.

---

### Tip 69: Añade Comandos a una Macro

Si grabaste una macro pero olvidaste un paso, no es necesario repetir todo:

    qA           " Comienza a añadir al registro 'a'
    j            " Añade el comando faltante
    q            " Finaliza

Esto evita tener que volver a grabar desde cero.

---

### Tip 70: Aplica una Macro a un Conjunto de Archivos

Puedes aplicar una macro sobre varios archivos con:

    :args *.md
    :argdo normal @a

Esto es especialmente útil para procesar lotes de archivos con un mismo patrón de edición.

---

### Tip 71: Usa un Iterador para Numerar Ítems

Para insertar números consecutivos:

    :let i=1
    :g/^/execute "normal I" . i . ". " | let i += 1

Alternativamente, usa una macro que incremente con `Ctrl-A`:

    qaI1. <Esc>^Aq
    10@a

Esto produce:

    1. texto
    2. texto
    ...

---

### Tip 72: Edita el Contenido de una Macro

Puedes pegar el contenido de una macro en el buffer, editarlo, y luego reinyectarlo:

    "ap      " Pega contenido del registro 'a'
    (edita directamente)
    "ay$     " Vuelve a copiarlo sin salto de línea

Esto permite refinar secuencias complejas sin tener que repetir la grabación.

---

Este capítulo enseña a grabar, ejecutar y manipular macros como una poderosa herramienta de automatización dentro de Vim. Con práctica, las macros pueden reducir tareas largas a unas pocas teclas.

