---
tags:
  - react
  - custom-hooks
---
Los custom hooks cumplen con una situación a menudo regular cuando estamos desarrollando en react, esto es poder adaptar el sistema a nuestras necesidades.

Estos custom, son creaciones nuestras con el fin de generar un código mas limpio y mantenible teniendo reunido diferentes situaciones relacionadas a un solo tema en una sola función. Ejemplo seria usar una llamada a una api, esta requiere la llamada propiamente dicha, la verificación de la respuesta y sus sucesivas acciones. Para esto necesitaríamos crear varios states así como ifs y demás, pero si llevamos esta lógica a un custom hook, podemos reducir y ordenar de mejor manera el código puesto.