# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 2: Modo Normal

El modo Normal es el estado natural de reposo en Vim. Si este capítulo te parece sorprendentemente corto, es porque gran parte del libro trata sobre cómo usar el modo Normal. Aquí, sin embargo, cubriremos algunos conceptos fundamentales y consejos generales.

Otros editores de texto pasan la mayor parte del tiempo en algo parecido al modo Insert. Para quienes se inician en Vim, puede parecer extraño que el modo Normal sea el predeterminado. En el Tip 7, comenzamos a explicar por qué, usando una analogía con el espacio de trabajo de un pintor.

---

### Tip 7: Detente con el Pincel Fuera del Lienzo

Para quien no está acostumbrado a Vim, el modo Normal puede parecer una elección rara como modo por defecto. Pero los usuarios experimentados de Vim no lo imaginan de otra manera.

¿Cuánto tiempo pasa realmente un pintor con el pincel tocando el lienzo? La mayor parte del tiempo está observando, mezclando colores, ajustando la luz… De igual forma, el programador pasa más tiempo pensando, leyendo, navegando. No es necesario estar todo el tiempo en modo Insert. Desde el modo Normal podemos mover, duplicar, reformatear o eliminar código.

---

### Tip 8: Agrupa Tus Deshacer

En otros editores, usar "deshacer" borra un solo carácter o palabra. En Vim, puedes controlar qué tan "grueso" es un bloque de deshacer.

Presiona `u` para deshacer el último cambio. Ese cambio puede provenir de cualquier modo (Normal, Visual o Command-Line). Si haces varios cambios pequeños pero quieres deshacerlos como un solo grupo, usa `:undojoin` entre ellos (o no salgas del modo Insert para mantenerlos unidos).

---

### Tip 9: Crea Cambios Repetibles

Evita hacer cambios únicos que no puedas repetir con `.`. Es mejor diseñar tus acciones para que puedan ser repetidas. Por ejemplo:

    f. r! ;. ;.

Busca el punto (`.`), reemplázalo por `!`, y repite dos veces. Este patrón se puede aplicar para muchos tipos de cambios simples.

---

### Tip 10: Usa Contadores para Aritmética Simple

Vim tiene comandos especiales `Ctrl-A` y `Ctrl-X` que incrementan o decrementan números.

    42<C-A>      → 43
    9<C-X>       → 8

También puedes usar prefijos numéricos:

    5<C-A>       → suma 5 (42 → 47)

Esto funciona sobre cualquier número bajo el cursor, sin necesidad de seleccionar.

---

### Tip 11: No Cuentes Si Puedes Repetir

Supón que quieres borrar 7 palabras. Podrías usar:

    d7w          " contar
    dw......     " o repetir con punto

Contar es preciso, pero lento. Repetir con `.` puede ser más natural y mantener un historial de deshacer más limpio.

---

### Tip 12: Combina y Conquista

Gran parte del poder de Vim está en combinar operadores con movimientos.

Ejemplos:

    dl          " borrar letra
    daw         " borrar palabra
    dap         " borrar párrafo
    y$          " copiar hasta final de línea

Estos comandos siguen la fórmula: **operador + movimiento = acción**.

Aprender más operadores y movimientos es como aprender más palabras en el vocabulario de Vim. Combinarlos te permite construir comandos más poderosos con pocas teclas.

---

**Nota sobre el Modo de Espera de Operador (Operator-Pending Mode):**

Cuando presionas `d`, Vim entra en un modo especial esperando el siguiente movimiento. Solo cuando presionas una tecla de movimiento como `w`, `j`, `}` se ejecuta el comando completo. Es un modo temporal entre acciones. Puedes cancelarlo con `<Esc>`.

---

