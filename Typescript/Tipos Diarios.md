---
tags:
 -typescript
 -types
---

# Tipos de datos en Typescript

## Tipos Básicos
- String: "Hello World".
- Number: 24, 3, 45.
- Boolean: true || false.

Los tipos "String, Number, Boolean " estos que aparecen con su letra inicial en mayúsculas son especiales. Usa siempre string, number y boolean.

## Arrays
- []number : Así definiríamos un array.
- Array<number> Esta es otra definición que también es valida.

### Any
Este tipo de dato permite el uso de cualquier otro tipo de dato, este mismo se usa cuando no hay claridad sobre el dato a usar 
y se pretende hacer que typescript pase de largo, debería ser usado solo temporalmente para así poder tener claro el tipo de 
dato a usar.

```ts
let obj: any = {x: 0}

obj.foo();
obj();
obj.bar = 100;
obj = "hello";
const n: number = obj;
```

## noImplicitAny
Esta bandera nos permite usar los tipos any a la hora de compilar ts, ya que por defecto este los identifica como un error.

## Type Annotation en Variables
Usar la anotación de tipos en una variable no suele ser necesario ya que ts lo hace automaticamente, pero
por semantica puede llegar a ser util si el código no permite distinguir claramente el tipo de la misma. 
Por eso existe esta opción:

```ts
let myName : string = "Jeison"

```
## Functions
Para las funciones ts permite agregar los tipos para los valores de entrada y salida.

### Parameters
En los parametros se definiria como una variable pero dentro del parentesis:

```ts
function greeter(name:string) {
    console.log("Hello, " + namej.toUpperCase() + "!!")
}
```
### Return Type Annotations
- Usualmente ocurre lo mismo que cuando declaramos variables, ts por defecto infiere el tipo de sentencia de retorno.
- Se puede llegar a encontrar una declaración explicita del retorno de la función en la documentación para propositos de aclaración.

Para los valores de salida o el valor de retorno seria así:
```ts
function getFavoriteNumber():number {
    return 26
}
```

### Functions Which Returns Promises
Para funciones que retornan un valor de tipo **Promesa**, puedes asignarla de la siguiente manera. Donde puedes notar el tipo number,
puedes cambiarlo para adaptarlo a tu necesidad:

```ts
async function getFavoriteNumber (): Promise<number> {
    return 26;
}
```
### Annonymous Functions 
- Las ***Funciones Anonimas*** son funciones que no son declaradas pero que se usan en base a ciertos espacios,
un ejemplo para esto es cuando usamos una arrow function dentro de un foreach. Dentro del foreach esta arrow function
no necesita de una declaración dentro de este espacio, así, este espacio se llama contexto.
- Mencionamos esto porque para este tipo de funciones ahi un tipado inferido por ts el cual depende de este contexto,
así pues lo llamamos ***Contextual Typing***. Este tipado solo se aplicara en espacios como este donde ts puede inferir
el resultado por el contexto.

```ts
const names = ["Alice", "Bob", "Eve"]

// Contextual Typing dentro de una funcion anonima
names.forEach(function (nameInFunction) {
    console.log(nameInFunction.toUpperCase())
})

names.forEach((nameInArrow) =>{
    console.log(nameInArrow.toUpperCase())
})
```
## Objects Types 
Refiere de los valores que contienen propiedades en si mismo.He aqui un ejemplo:

```ts

//Aqui podemos ver como definiriamos los diferentes tipos dentro de un objeto al implementarlo
// dentro de una función
function printCoord(pt: {x:number; y:number}) {
    console.log("The coordinate's x value is: " + pt.x)
    console.log("The coordinate's y value is: " + pt.y)
}
printCoord({x:3, y: 7})
```
- El tipo para cada propiedad es opcional, si no se define, esta pasara a ser "any".

### Optional Properties
Usar una propiedad opcional tiene sus desventajas, dentro de esas esta el hecho de manejar un valor indefinido,
en js normalmente se interpretara así, pero recuerda siempre verificar y filtrar estos tipos de valores.

- Para indicar que una propiedad es opcional usaremos el "?" antes de poner el ':' del tipado

```ts

function printName(obj: { first: string; last?:}) {
    console.log(obj.last.toUpperCase());
    //Aqui tendremos el mensaje de manejo indefinido de la propiedad
    if(obj.last !== undefined){
        //Buscamos verificar la propiedad
        console.log(obj.last.toUpperCase());
    }
    // Una alternativa mas segura
    console.log(obj.last?.toUpperCase());
}

```
### Union Types
- Unión de dos o mas tipos de datos, los cuales pueden ser recibidos en una variable.
- El sentido de esta propiedad es poder tener la capacidad de operar con diferentes tipos de manera restringida
y en base a nuestras necesidades.
- Podremos usar funciones unicas de cada tipo, teniendo cuidado de filtrarlo. TS se dara cuenta si no lo hacemos.

```ts

function printId(id: number | string) {
  if (typeof id === "string") {
    // Aqui filtramos aquellos que son 'string'
    console.log(id.toUpperCase());
  } else {
    // Aqui tienen que ser tipo number 'number'
    console.log(id);
  }
}
```
```ts 

function welcomePeople(x: string[] | string) {
  if (Array.isArray(x)) {
    // Here: 'x' is 'string[]'
    console.log("Hello, " + x.join(" and "));
  } else {
    // Here: 'x' is 'string'
    console.log("Welcome lone traveler " + x);
  }
}
```

### Types Aliases
- Esto no es mas que una forma de definir caracteristicas en una variable que se desean usar mas de uan vez.
- Se puede representar como un objeto, así como con union types.
- Al usar un type para definir una variable, esta puede seguir usando el tipo de variable definido al usar este tipo,
sin ser asignado.

```ts 
type Point = {
  x: number;
  y: number;
};
 
// Exactly the same as the earlier example
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

```ts 
type UserInputSanitizedString = string;
 
function sanitizeInput(str: string): UserInputSanitizedString {
  return sanitize(str);
}
 
// Create a sanitized input
let userInput = sanitizeInput(getInput());
 
// Puede ser asignada como un string otravez
userInput = "new input";
```

### Interfaces
- Las interfaces son tambien otra forma de definir tipos agrupados( objetos anonimos) para usos repetitivos.
- Se puede extender con otras intefaces, los tipos tambien pero en su caso es una intersección.
- Se puede modificar despues de ser creada, a diferencia de los tipos.

```ts 
interface Point {
  x: number;
  y: number;
}
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

### Type Assertions
- Son una forma de agregar información sobre una instancia que puede no ser reconocida por ts, tal como tipos mas especificos de
ciertos tipos de variables.
- Se usa tanto para agregar como para delimitar la información que necesita ts de una instancia en concreto.

```ts
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;//Agregando informacion

const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");//Así usando otra estandarización

const a = expr as any as T; // Esta es para ciertas situaciones donde agregar la aserción genera problemas de coerción
// con otras funciones.

```

### Literal Types
- Un tipo literal en TypeScript representa un valor exacto (por ejemplo "Hola", 42 o true) en lugar de un conjunto más amplio de valores (string, number, boolean). Se usan principalmente en combinación con uniones para restringir un valor a un conjunto fijo de opciones válidas.


### Undefined and null types

- Tanto null como undefined tienen la misma definicion. Esta seria la de
un valor ausente o no inicializado.
- Cuando "strictNullChecks" este apagado, tanto null como undefined 
podran ser usados sin generar mayor incoveniente o error en el codigo.
- Cuando "strictNullChecks" este activado, ts no permitira el 
uso de null o undefined sin una condicional de verificación 
de las mismas en el codigo.
- Puedes omitir la verificación de estos dos tipos al usar "!" antes de las mismas.

```ts
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```

### Enums
- Nos permite escojer un valor de un set de constantes dentro del codigo.
- Se tratara mas sobre este tipo de valor mas adelante.

### Less Common Primitives

- bigint: Para enteros muy largos
- symbol: Para crear un identificador unico atraves de la función "Symbol()"
