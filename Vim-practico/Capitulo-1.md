# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 1: El Camino Vim

Nuestro trabajo es repetitivo por naturaleza. Ya sea haciendo el mismo cambio pequeño en varios lugares o moviéndonos entre regiones similares de un documento, repetimos muchas acciones. Cualquier cosa que agilice ese flujo de trabajo repetitivo ahorrará tiempo en gran medida.

Vim está optimizado para la repetición. Su eficiencia proviene de cómo rastrea nuestras acciones recientes. Siempre podemos repetir el último cambio con una sola tecla. Pero eso solo es útil si aprendemos a diseñar nuestras acciones de modo que tengan valor al ser repetidas. Dominar este concepto es clave para volverse efectivo en Vim.

---

### Tip 1: Conoce el Comando Punto

El comando punto (`.`) repite el último cambio. Es el comando más poderoso y versátil de Vim.

**Ejemplo en Vim script:**
```vim
    " Eliminar tres palabras consecutivas
    daw  " Elimina la palabra actual
    .    " Repite en la siguiente palabra
    .    " Repite nuevamente
```
---

### Tip 2: No Te Repitas (DRY)

Contexto JavaScript:
```js
    var foo = 1
    var bar = 'a'
    var foobar = foo + bar
```
Solución en Vim:
```vim
    A;<Esc>  " Insertar ';' al final de línea actual
    j.       " Saltar abajo + repetir comando punto
    j.       " Repetir en siguiente línea
```
---

### Tip 3: Retrocede un Paso, Luego Avanza Tres

Contexto JavaScript:
```js
    method("+argument1+","+argument2+")
```
Solución Vim:
```vim
    f+        " Buscar siguiente '+'
    s + <Esc> " Reemplazar carácter con ' + '
    ;.        " Repetir búsqueda + comando punto
    ;.        " Repetir nuevamente
```
---

### Tip 4: Actúa, Repite, Revierte

Comandos repetibles y sus reversos:

| Intención         | Actuar          | Repetir | Revertir |
|------------------|------------------|---------|----------|
| Hacer cambio     | iTexto<Esc>      | .       | u        |
| Buscar carácter  | f{char}          | ;       | ,        |
| Buscar patrón    | /patrón<CR>      | n       | N        |
| Sustituir        | :s/viejo/nuevo   | &       | u        |

---

### Tip 5: Buscar y Reemplazar Manualmente

**Texto de ejemplo:**

Esperando contenido antes del lanzamiento...  
Si estás contento con esto, continuemos...  
Lanzaremos cuando tengamos el contenido...

Flujo Vim:
```vim
    *            " Buscar palabra bajo cursor (content)
    cwcopy<Esc>  " Cambiar a 'copy'
    n            " Siguiente ocurrencia
    .            " Aplicar cambio
```
---

### Tip 6: Fórmula del Punto

Patrón óptimo: 1 tecla para moverse + 1 tecla para ejecutar

| Tarea                 | Movimiento | Acción |
|----------------------|------------|--------|
| Añadir ';' al final  | j          | .      |
| Espaciar operadores  | ;          | .      |
| Cambiar palabras     | n          | .      |

Este patrón se repite constantemente: mover + ejecutar. ¡Altamente eficiente!

