# Que es  eso de zero y few shot?
Define la calidad y profundidad de la instrucción que le damos al llm para desarrollar una tarea, la diferencia mas obvia reside en el contenido de esta instrucción.

## Zero shot
Es en base una instrucción corta, no quiere decir que sea casi nula, refiere a la cantidad de contexto o de ejemplos que se suguieren al llm para que tome como ejemplos, en este caso seria pocos o ninguno.

## Few shot
En este definimos una cantidad amplia de ejemplos, pero "amplio" generaliza bastante. En efecto, es porque cada caso puede requerir de diferentes cantidades de ejemplos y considerar una cantidad base no es apropiado

## Ejemplos?
Los ejemplos dependen del resultado esperado y requiere de evaluar que casos pueden generar un contexto apropiado y reducir la ambiguedad de los resultados al mostrar varias situaciones o casos que plantean diferentes situaciones y su correspondiente valor para la instruccion

- Lo apropiado o recomendado es usar entre 3 y 7 ejemplos
- El orden importa, y logra afectar entre un 50% y 90% 
- Usar ejemplos intercalados seria lo recomendado.

## Zero ó Few?
- ¿ Hay ambiguedad en la tarea?
- ¿ Es compleja?
- ¿ Necesita presición o replicación?

Si para las tres es SI, lo natural es usar few, pero aconsejan probar los 2.
