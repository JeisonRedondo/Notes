# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 3: Modo Insert

La mayoría de los comandos de Vim se activan desde otros modos, pero algunas funcionalidades están al alcance directo desde el modo Insert. En este capítulo, exploramos esos comandos.

Aunque `delete`, `yank` y `put` se usan desde el modo Normal, hay un atajo para pegar texto desde un registro sin salir del modo Insert. También aprenderemos dos formas para insertar caracteres especiales que no están en el teclado.

El modo Replace es un caso especial del modo Insert, en el que los caracteres reemplazan los existentes. Veremos cómo invocarlo y en qué situaciones es útil. También conoceremos el modo **Insert Normal**, que permite ejecutar un solo comando en modo Normal antes de regresar a Insert.

La autocompletación es lo más avanzado dentro del modo Insert, pero eso se cubrirá más adelante, en el Capítulo 19.

---

### Tip 13: Corrige al Instante Desde el Modo Insert

Si cometemos un error al escribir, podemos corregirlo inmediatamente sin cambiar de modo.

Los mecanógrafos expertos recomiendan borrar toda la palabra mal escrita y volverla a escribir. Si escribes más de 60 palabras por minuto, reescribirla tomará solo un segundo. Si no, considéralo una buena práctica.

Podrías cambiar al modo Normal, moverte al inicio de la palabra, corregirla y volver al Insert con `A`, pero eso toma más tiempo. Mejor quédate en Insert.

Comandos útiles:

| Acción                              | Tecla       |
|-------------------------------------|-------------|
| Borrar un carácter                  | `<C-h>`     |
| Borrar una palabra                  | `<C-w>`     |
| Borrar hasta el inicio de la línea  | `<C-u>`     |

---

### Tip 14: Regresa al Modo Normal

El modo Insert sirve para una tarea: **escribir texto**. El modo Normal es donde realmente trabajamos, así que debemos cambiar entre ellos fácilmente.

| Acción                            | Tecla      |
|----------------------------------|------------|
| Salir a modo Normal              | `<Esc>`    |
| Alternativa a `<Esc>`            | `<C-[>`    |
| Ejecutar un solo comando Normal  | `<C-o>`    |

`<C-o>` activa el modo **Insert Normal**, ejecuta un solo comando (como `zz`) y vuelve a Insert inmediatamente. Ideal para mantener el ritmo.

---

### Tip 15: Pega desde un Registro sin Salir de Insert

Queremos insertar texto que ya está al inicio de un archivo en la línea actual sin salir del modo Insert:

    yt,          " yankeamos hasta la coma
    jA␣          " nos movemos abajo y entramos al final
    <C-r>0       " pegamos el registro 0
    .<Esc>       " añadimos punto final

Este método evita salir de Insert. Se hablará más sobre registros en el capítulo 10.

---

### Tip 16: Haz Cálculos Rápidos en Insert

Puedes usar `<C-r>=` seguido de una expresión para insertar el resultado directamente:

    <C-r>=5*3<CR>     → inserta 15
    <C-r>=strftime("%Y")<CR>   → inserta el año actual

Esto accede al "registro de expresión", útil para cálculos rápidos sin salir de Insert.

---

### Tip 17: Inserta Caracteres Inusuales por Código

Desde Insert, puedes usar combinaciones con `<C-v>`:

| Acción                                   | Tecla               |
|------------------------------------------|---------------------|
| Carácter por código decimal              | `<C-v>123`          |
| Carácter por código hexadecimal          | `<C-v>u1234`        |
| Insertar carácter literal (no dígito)    | `<C-v>{no-dígito}`  |

Ejemplo: `<C-v><Tab>` inserta un **tab real** sin importar la opción `expandtab`.

---

### Tip 18: Inserta Caracteres Inusuales por Dígrafo

dígrafos: pares de letras que representan un carácter especial. Ejemplos:

| Carácter | Dígrafo |
|----------|---------|
| ¿        | `?I`    |
| « »      | `<< >>` |
| ½ ¼ ¾    | `12 14 34` |

desde Insert, escribe `<C-k>{char1}{char2}`. Por ejemplo:

    <C-k>?I      → inserta ¿

puedes consultar todos los disponibles con `:digraphs`.

---

### Tip 19: Sobrescribe Texto con el Modo Replace

el modo Replace (`R`) sobrescribe texto en vez de insertarlo. Ejemplo:

texto:

    Typing in Insert mode extends the line. But in Replace mode the line length doesn't change.

acción:

    R,          → reemplaza el punto por coma
    lrb         → escribe "but" en minúscula
    <Esc>

resultado:

    Typing in Insert mode extends the line, but in Replace mode the line length doesn't change.

ideal para ajustes pequeños sin borrar y reescribir todo.

