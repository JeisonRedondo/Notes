---
- react
---
# React - Client Side Routing

## Ventajas
- Client Side Routing cambia la vista usando JS y el History API, evitando una recarga completa.
- Aumenta la velocidad de visualización de la pagina.

## Nested Routes
- Las nested routes permiten que distintas partes de la UI cambien según la URL, compartiendo layouts.
## Link
- Permite manejar la navegación entre componentes sin recargar la pagina, manteniendo los estados de la pagina
- "desacopla la navegación del servidor, permitiendo que el cliente controle el cambio de vistas y conserve el estado interno de React."

### ¿... y que pasaria con una <a href...>?
- Esta etiqueta genera una petición al servidor, lo cual recargara la pagina.
- Genera carga en la aplicación y tambien reinicia todos los estados.

## Dynamic Segment
- Usualmente un segmento dinamico referencia una ruta(path)
- Permite crear rutas variables
- Rutas que se actualizan basado en los parametros asignados

### loader
- Puedes proveer información(data) a un route a traves de un loader
- Esta información cargara antes de qeu se renderize el componente.


### action
- Permite actualizar los datos de el componente al iniciar una acción, la cual reacciona al usuario. Puede cargar pequenos pedazos de HTML y HTTP
### params
- Permite obtener información relacionada con la url actual y que coincidio para ser usada en esta pagina

### useMatch
- Verifica que la ruta coincide con un patron
