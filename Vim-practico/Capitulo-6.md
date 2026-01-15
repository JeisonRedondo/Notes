# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 6: Manejar Múltiples Archivos

Vim nos permite trabajar con múltiples archivos al mismo tiempo. La lista de búferes ayuda a mantener el control de los archivos abiertos en una sesión. Además, contamos con herramientas como ventanas divididas, pestañas y la lista de argumentos para navegar entre ellos con eficiencia.

---

### Tip 37: Rastrea Archivos Abiertos con la Lista de Búferes

Cuando abres un archivo en Vim, su contenido se carga en un búfer. Los cambios que haces se aplican al búfer, no directamente al archivo en disco.

    :ls            " Lista los búferes abiertos
    :bnext         " Ir al siguiente búfer
    :bprev         " Ir al búfer anterior
    <C-^>          " Volver al búfer anterior

Mapeos comunes (por ejemplo, usando unimpaired.vim):

    [b             " búfer anterior
    ]b             " búfer siguiente
    [B             " primer búfer
    ]B             " último búfer

---

### Tip 38: Agrupa Búferes con la Lista de Argumentos

La lista de argumentos contiene los archivos que pasarías como parámetros al iniciar Vim.

    :args *.js
    :argdo %s/foo/bar/g

También puedes usar patrones complejos o listas generadas:

    :args **/*.js **/*.css
    :args `cat .archivos`

La ventaja es aplicar comandos a todos los archivos en `:args` sin afectar otros búferes cargados.

---

### Tip 39: Gestiona Archivos Modificados

Con la opción `set hidden`, puedes cambiar de búfer sin necesidad de guardar.

    :set hidden
    :bnext

Comandos comunes para manejar cambios:

| Acción                         | Comando   |
|--------------------------------|-----------|
| Guardar cambios                | :write    |
| Revertir a versión en disco    | :edit!    |
| Salir sin guardar              | :qall!    |
| Guardar todos los búferes      | :wall     |

---

### Tip 40: Divide el Espacio con Ventanas

Vim permite dividir la pantalla en varias ventanas para ver múltiples archivos o secciones simultáneamente.

    :split archivo.txt        " división horizontal
    :vsplit otro.txt          " división vertical

Movimientos entre ventanas:

    <C-w>w     " siguiente ventana
    <C-w>h     " mover izquierda
    <C-w>l     " mover derecha
    <C-w>j     " mover abajo
    <C-w>k     " mover arriba

---

### Tip 41: Organiza Ventanas con Pestañas

Las pestañas agrupan una o más ventanas. No son como en navegadores; piénsalo como "layouts" de ventanas.

    :tabnew archivo.txt
    <C-w>T             " mover ventana actual a nueva pestaña
    :tabclose          " cerrar pestaña actual
    :tabonly           " cerrar todas excepto la actual

Navegación entre pestañas:

    gt      " siguiente pestaña
    gT      " pestaña anterior
    :tabn N " ir a pestaña número N

---

Este capítulo permite usar Vim como un entorno de edición completo para múltiples archivos, muy útil para proyectos grandes o tareas paralelas.
