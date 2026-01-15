# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 8: Navegar Dentro de Archivos con Movimientos

Los movimientos son comandos fundamentales en Vim. No solo te permiten mover el cursor, sino que también determinan el alcance de operaciones como borrar, copiar y cambiar. Este capítulo cubre varios tipos de movimientos y cómo usarlos eficientemente.

---

### Tip 47: Mantén los Dedos en la Línea Base

Vim está optimizado para mecanógrafos táctiles. Usa `h`, `j`, `k`, `l` para moverte sin alejar las manos de la fila base.

    h  ← izquierda
    l  → derecha
    j  ↓ abajo
    k  ↑ arriba

Reasigna las flechas para no depender de ellas:

    noremap <Up> <Nop>
    noremap <Down> <Nop>
    noremap <Left> <Nop>
    noremap <Right> <Nop>

---

### Tip 48: Distingue Entre Líneas Reales y Líneas Visuales

Una *línea real* termina con un salto de línea. Una *línea visual* es como se presenta en pantalla (puede estar envuelta).

Usa `gk` y `gj` para navegar por líneas visuales cuando `'wrap'` está activo:

    j     → línea real abajo
    gj    → línea visual abajo
    k     → línea real arriba
    gk    → línea visual arriba

---

### Tip 49: Muévete por Palabras

Mueve el cursor una palabra a la vez:

    w   → siguiente inicio de palabra
    e   → final de palabra
    b   → inicio de palabra anterior

Para palabras tipo `snake_case` o `camelCase`, puedes personalizar `'iskeyword'`.

Distingue entre `w` y `W`:

    w / b / e   → ignoran puntuación
    W / B / E   → saltan bloques separados por espacios

---

### Tip 50: Encuentra Caracteres

Para moverte con precisión en una línea:

    f<char>    → encuentra el carácter hacia adelante
    F<char>    → hacia atrás
    t<char>    → antes del carácter
    T<char>    → después del carácter

Usa `;` para repetir y `,` para retroceder.

---

### Tip 51: Usa Búsqueda para Navegar

Búsqueda básica:

    /texto<CR>     → busca adelante
    ?texto<CR>     → busca atrás
    n / N          → siguiente / anterior ocurrencia

Se puede usar como movimiento en comandos como `d/palabra<CR>`.

---

### Tip 52: Selecciona con Objetos de Texto

Ejemplos:

    ciw    → cambiar palabra actual
    di(    → borrar dentro de paréntesis
    da"    → borrar alrededor de comillas
  esto esta afuera (esto esta adentro) afuera de las comillas "dentro de comillas"
Composición:

| Objeto de texto     | Dentro (`i`) | Alrededor (`a`) |
|---------------------|--------------|-----------------|
| palabra             | iw           | aw              |
| frase               | is           | as              |
| párrafo             | ip           | ap              |
| entre paréntesis    | i(           | a(              |
| entre comillas      | i"           | a"              |

---

### Tip 53: Borra Alrededor o Cambia Dentro

Usa `d` para borrar y `c` para cambiar:

    daw      → borrar palabra y espacio
    ciw      → cambiar palabra sin espacio

La diferencia es útil según el contexto: `daw` deja limpio, `ciw` te permite reemplazar contenido sin desorden.

---

### Tip 54: Marca tu Lugar y Regresa

Usa marcas para volver a ubicaciones específicas:

    m{letra}     → marca en el archivo
    `{letra}     → ir a la posición exacta
    '{letra}     → ir al inicio de la línea marcada

También puedes usar `` `` y `''` para volver a la última posición de salto.

---

### Tip 55: Salta Entre Paréntesis Emparejados

    %   → salta entre `{}`, `[]`, `()` emparejados

Funciona dentro de bloques anidados. Muy útil al editar código estructurado.

---

Este capítulo muestra cómo dominar los movimientos te convierte en un editor de texto eficiente. Cuanto mejor conozcas las combinaciones, más control tendrás del texto.

