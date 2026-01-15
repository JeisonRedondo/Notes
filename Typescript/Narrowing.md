---
tags:
 - typescript
 - narrowing
---

# Narrowing

- El narrowing es definido como la practica en la cual condicionamos el flujo de el codigo en base a ciertos tipo de valores.
- Se basa en el "Type Guard" el cual es la acción de generar una condición para verificar si un valor es de un
  tipo de dato en especifico.
- Ahi una lista en la que se basa los type guards para poder permitir las acciones:
  - "string"
  - "number"
  - "bigint"
  - "boolean"
  - "symbol"
  - "undefined"
  - "object"
  - "function"

Esta practica tiene una función en especifico en ts, la cual es verificar que no se den tipos de datos no verificados o ausentes dentro
del codigo, lo cual puede dar espacio a un undefined o un null.

Para explicar mas claramente cada una de las situaciones en las que se puede desarrollar el narrowing veremos cada una:

### typeof **Narrowing**

- Reduce el tipo cuano usas "typeof" usando condicionales para poder cersiorarse del tipado especifico.

```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    // Aquí TS ya sabe que id es un string
    console.log("El id en mayúsculas:", id.toUpperCase());
  } else {
    // Si no es string, solo puede ser number
    console.log("El id en número:", id.toFixed(2));
  }
}
```

### instanceof **Narrowing**
- Se usa especialmente cuando construimos con "new": 

```ts
class Dog {
  bark() { console.log("Woof!"); }
}
class Cat {
  meow() { console.log("Meow!"); }
}

function makeSound(pet: Dog | Cat) {
  if (pet instanceof Dog) {
    pet.bark(); // TS sabe que es Dog
  } else {
    pet.meow(); // TS sabe que es Cat
  }
}

```

### "in" operator **Narrowing**
- Se usa principalmente con objetos que tienen propiedades que difieren unas de otras: 

```ts
type Car = { wheels: number; drive: () => void };
type Boat = { propeller: number; sail: () => void };

function move(vehicle: Car | Boat) {
  if ("wheels" in vehicle) {
    vehicle.drive(); // TS sabe que es Car
  } else {
    vehicle.sail(); // TS sabe que es Boat
  }
}

```


### Truthiness **Narrowing**
-  Se usa principalmente para verificar que un argumento no tenga valores nulos tales como null, undefined
0, "", false:

```ts
function printLength(str?: string) {
  if (str) {
    console.log("Longitud:", str.length); // Aquí str no puede ser undefined ni null
  } else {
    console.log("No se recibió cadena");
  }
}



```
### Equality **Narrowing**
- Inicialmente se usa generando comparaciones de valores con == o != e incluso con switch:

```ts
type Direction = "up" | "down" | "left" | "right";

function move(direction: Direction) {
  if (direction === "up" || direction === "down") {
    console.log("Movimiento vertical");
  } else {
    console.log("Movimiento horizontal");
  }
}

```
### type predicates **Narrowing**
- Usado con funciones que generan acciones que se asemejan a type guards:

```ts 
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

function move(pet: Fish | Bird) {
  if (isFish(pet)) {
    pet.swim(); // TS sabe que es Fish
  } else {
    pet.fly(); // TS sabe que es Bird
  }
}


```
### Discriminated unions **Narrowing**
- Para esta vez usaremos una propiedad de los objetos, "kind" la cual al asignarla podemos tanto cambiar como verificar para poder discriminar entre ciertos objetos:

```ts
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number };

function area(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side * shape.side;
  }
}

```
### Exhaustiveness checking **Narrowing**
- Esta es similar a la anterior solo que en esta dinamica nos aseguramos de manejar los posibles errores:

```ts 
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side * shape.side;
    default:
      const _exhaustiveCheck: never = shape; // Error si falta un caso
      return _exhaustiveCheck;
  }
}


```
