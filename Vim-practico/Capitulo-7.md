# Practical Vim - Edición Española  
**Editar Texto a la Velocidad del Pensamiento**  
*Segunda Edición*  
**Drew Neil**  
Prólogo de Tim Pope  

---

## Capítulo 7: Abrir Archivos y Guardarlos en Disco

Vim ofrece múltiples formas de abrir y guardar archivos, incluyendo exploración del sistema de archivos y comandos Ex para manipular rutas y permisos. Este capítulo aborda cómo trabajar con archivos de forma eficiente dentro del flujo de Vim.

---

### Tip 42: Abrir un Archivo por su Ruta con `:edit`

El comando `:edit` permite abrir archivos usando rutas absolutas o relativas.

    :edit ./ruta/archivo.txt
    :e ~/documentos/notas.md

También puedes usar `%:h` para referirte al directorio del archivo actual:

    :edit %:h/otro.md

Usa `:pwd` para ver el directorio de trabajo actual y `:cd` para cambiarlo.

---

### Tip 43: Abrir un Archivo por su Nombre con `:find`

Si configuras correctamente la opción `'path'`, puedes usar `:find` para buscar archivos sin especificar la ruta completa.

    :set path+=**
    :find app.js

Esto es útil en proyectos grandes donde los archivos están distribuidos en varios subdirectorios.

Autocompletado con `<Tab>` funciona perfectamente con `:find` una vez configurado `'path'`.

---

### Tip 44: Explorar el Sistema de Archivos con netrw

Vim incluye el plugin `netrw`, que permite navegar y editar archivos como si fuera un administrador de archivos.

    :Explore       " Abre el explorador en el directorio actual
    :Sexplore      " Divide ventana horizontalmente y abre netrw
    :Vexplore      " Divide verticalmente

Desde ahí puedes navegar con `hjkl`, abrir archivos con `<CR>`, renombrar con `R`, borrar con `D`, y más.

También puedes usar netrw para acceder a archivos remotos vía FTP, scp, etc.

---

### Tip 45: Guardar Archivos en Directorios Inexistentes

Si intentas guardar un archivo en una ruta que no existe, obtendrás un error como:

    E212: Can't open file for writing

Para solucionarlo, crea la ruta primero desde Vim:

    :!mkdir -p %:h
    :write

`%:h` representa el directorio del archivo actual.

---

### Tip 46: Guardar un Archivo como Superusuario

A veces necesitas guardar un archivo que requiere permisos de superusuario, como `/etc/hosts`.

En lugar de reiniciar Vim con `sudo`, puedes usar:

    :w !sudo tee % > /dev/null

Esto guarda el búfer actual como root. Vim pedirá tu contraseña y usará `sudo` externamente.

---

Este capítulo te enseña a abrir, explorar y guardar archivos de forma flexible en Vim, incluso cuando las condiciones del sistema lo dificultan. Ideal para trabajar en entornos Unix o en proyectos complejos.
