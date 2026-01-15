---
tags:
  - function
  - typescript
---

# More on Functions

## Function Type Expressions
- Para agregarle un typo a la funcion simplemente las ubicamos para los parametros, despues del ":" y para el retorno de
la función al lado también usando ":".
```ts
function greeter(fn: (a: string) => void) {
  fn("Hello, World");
}
 
function printToConsole(s: string) {
  console.log(s);
}
 
greeter(printToConsole);
```
- La sintaxis que se usa en la función anonima indica que se ingresara un parametro con nombre "a", de tipo "string", y que esta funcion
tendra una salida tipo "void", esto significa que sera vacia o que no se espera salida.
- Si el tipo no es especificado este se intrepretara como un tipo "any" por defecto.
- También podemos usar un type para poder definir mas comodamente la función a ingresar.

```ts
type GreetFunction = (a: string) => void;
function greeter(fn: GreetFunction) {
  // ...
}
```
## Call Signature
- La call signature es la caracteristica que describe la aplicación de typos en la creación de funciones en typescript, 
 donde usaremos typos tanto para parametros como para las devoluciones de las funciones. Esto se resalta porque es una dinamica,
 la cual se usa de distintas maneras, aplicando type para describir un ingreso de varios parametros en una función de manera ordenada
como para otras circunstancias.

```ts
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}
 
function myFunc(someArg: number) {
  return someArg > 3;
}
myFunc.description = "default description";
 
doSomething(myFunc);
```
## Construct Signature
- Esta caracteristica habla del uso puntual de  constructores que pueden ser invocados dentro de un type tal como vimos anteriormente,
y como son perfectamente usable tanto con el "new" como sin el.

```ts
interface CallOrConstruct {
  (n?: number): string;
  new (s: string): Date;
}
 
function fn(ctor: CallOrConstruct) {
  // Passing an argument of type `number` to `ctor` matches it against
  // the first definition in the `CallOrConstruct` interface.
  console.log(ctor(10));
               
(parameter) ctor: CallOrConstruct
(n?: number) => string
 
  // Similarly, passing an argument of type `string` to `ctor` matches it
  // against the second definition in the `CallOrConstruct` interface.
  console.log(new ctor("10"));
                   
(parameter) ctor: CallOrConstruct
new (s: string) => Date
}
 
fn(Date);

```

## Generic Functions
- permiten tener la capacidad de manejar diferentes tipos de datos
- se relacionan o pueden relacionarse los parametros junto con los argumentos y el retorno
- No necesitamos saber que tipo de dato se manejara mientras podamos contar con sus caracteristicas
```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}
```

### Inference
- Typescript al reaccionar al tipo y entender que tipo manejara la funcion, permite la ambiguedad de esta funcion

```ts
function map<Input, Output>(arr: Input[], func: (arg: Input) => Output): Output[] {
  return arr.map(func);
}
 
// Parameter 'n' is of type 'string'
// 'parsed' is of type 'number[]'
const parsed = map(["1", "2", "3"], (n) => parseInt(n));
```

### Constrainsts
- Las constrainst (restricciones) son una opción que nos permite filtrar ciertos tipos de datos con los que queremos trabajar.

```ts
function longest<Type extends { length: number }>(a: Type, b: Type) {
  if (a.length >= b.length) {
    return a;
  } else {
    return b;
  }
}
 
// longerArray is of type 'number[]'
const longerArray = longest([1, 2], [1, 2, 3]);
// longerString is of type 'alice' | 'bob'
const longerString = longest("alice", "bob");
// Error! Numbers don't have a 'length' property
const notOK = longest(10, 100);
Argument of type 'number' is not assignable to parameter of type '{ length: number; }'.
```


### Working with constrainst
- Ahí que recodar que cuando se trabaja con Funciones Genericas, debemos comprender donde estamos usando los tipos genericos,
y cuando. En el siguiente ejemplo se visualiza un error al intentar asignar un tipo number al retorno, donde ya se habia asignado el 
tipo generico. Esto genera un error al tratar de asumir que podremos asignar un numero a la salida que ya esta asignada unicamente
para recibir tipos genericos.

```ts
function minimumLength<Type extends { length: number }>(
  obj: Type,
  minimum: number
): Type {
  if (obj.length >= minimum) {
    return obj;
  } else {
    return { length: minimum };
Type '{ length: number; }' is not assignable to type 'Type'.
  '{ length: number; }' is assignable to the constraint of type 'Type', but 'Type' could be instantiated with a different subtype of constraint '{ length: number; }'.
  }
}
```

### Specifying Type Arguments
-  Al asignar en funciones genericas varios tipos de argumentos con diferentes tipos, podriamos dar por sentado que, 
ya que ts puede deducir el tipo de las mismas, esto se aplicara tambien a las asignaciones de los argumentos en la
funcion. Esto no sucede porque no seguiria la linea de control que por defecto usa ts, en la cual prioriza el control
de tipos. Entonces ts te pide que si asignaras ciertas variaciones en los argumentos, agreges estas variaciones a la asignación
 de las genericas.

 ```ts
function combine<Type>(arr1: Type[], arr2: Type[]): Type[] {
  return arr1.concat(arr2);
}

const arr = combine([1, 2, 3], ["hello"]);
Type 'string' is not assignable to type 'number'.

const arr = combine<string | number>([1, 2, 3], ["hello"]);
```

### Guideline for Writing Good Gereric Function
#### Push type parameters down
- Implica que tenemos que tener cuidado con como usamos el generico a la hora de implementarlo en las funciones,
tener cuidado de no hacer una implementación innecesaria de la misma:

```ts
function firstElement1<Type>(arr: Type[]) {
  return arr[0];
}
 
function firstElement2<Type extends any[]>(arr: Type) {
  return arr[0];
}
 
// a: number (good)
const a = firstElement1([1, 2, 3]);
// b: any (bad)
const b = firstElement2([1, 2, 3]);

```

#### Use Fewer Type Parameters
- Relacionar varios valores atraves del mismo tipo es la base, el no usarlo o no tenerle un uso a esa funcionalidad y aun asi implementarla
es problematico. Por eso es escencial saber donde y caund usarlo:

```ts
function filter1<Type>(arr: Type[], func: (arg: Type) => boolean): Type[] {
  return arr.filter(func);
}
 
function filter2<Type, Func extends (arg: Type) => boolean>(
  arr: Type[],
  func: Func
): Type[] {
  return arr.filter(func);
}
```

#### Type parameters should appear twice
- Ahi que recordar que las funciones genericas tienen usos especificos, no todas las funciones tienen que ser
tipo generico. Recuerda que para que haya uan posibilidad de usar el tipo generico se debe de 
necesitar su funcionalidad por lo menos dos veces.

```ts
function greet<Str extends string>(s: Str) {
  console.log("Hello, " + s);
}
 
greet("world");

function greet(s: string) {
  console.log("Hello, " + s);
}
```
### Optional Parameters
- Permite tener dos tipos diferentes asignables, de los caules uno de ellos es undefined. Esto para que nos perimta tener libertad para definirlo o no hacerlo dependiendo de la necesidad.

```ts
function f(n: number) {
  console.log(n.toFixed()); // 0 arguments
  console.log(n.toFixed(3)); // 1 argument
}

function f(x?: number) {
  // ...
}
f(); // OK
f(10); // OK

function f(x = 10) {
  // ...
}

// All OK
f();
f(10);
f(undefined);
```

#### Optional Parameters in Callbacks
- Podemos definirlas dentro de los argumentos que ingresaremos en el callback, y esto nos permite mantener opcional el ingreso del mismo.
- Para poder usarla debemos tener claro que tenemos que generar constraints claros a la hora de usarlas dentro de la función.

### Function overloads
- Estas funciones nos permiten llamar una función con una cierta variedad de argumentos, lo cual nos permite ajustar la ejecución de la
función en base a la cantidad de argumentos que ingresaremos a la funcion.

```ts
function makeDate(timestamp: number): Date;
function makeDate(m: number, d: number, y: number): Date;
function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
  if (d !== undefined && y !== undefined) {
    return new Date(y, mOrTimestamp, d);
  } else {
    return new Date(mOrTimestamp);
  }
}
const d1 = makeDate(12345678);
const d2 = makeDate(5, 5, 5);
const d3 = makeDate(1, 3);
No overload expects 2 arguments, but overloads do exist that expect either 1 or 3 arguments.

```

#### Overload Signature and the Implementation Signature
- Para poder implementar apropiadamente una función sobrecargada, tenemos que tener coherencia con el sentido de la función, esto quiere
decir que: 
    - El retorno de todas las variaciones debe ser el mismo, de no ser asi generar error:
    ```ts 
    function fn(x: string): void;
        function fn() {
          // ...
        }
        // Expected to be able to call with zero arguments
        fn();
        Expected 1 arguments, but got 0.

    ```
    - Debe tenerse en cuenta que los argumentos que se repitan deben ser del mismo tipo, o usar una definición diferente para ello:
    ```ts
        function fn(x: boolean): void;
        // Argument type isn't right
        function fn(x: string): void;
        This overload signature is not compatible with its implementation signature.
        function fn(x: boolean) {}
    ```
    - Lo mismo pasa con el return type, necesita ser coherente con el resto:
    ```ts
    function fn(x: string): string;
        // Return type isn't right
        function fn(x: number): boolean;
        This overload signature is not compatible with its implementation signature.
        function fn(x: string | number) {
          return "oops";
        }
    ```
#### Writting Good Overloads
- Implementar una funcion sobrecargada tiene su funcionalidad en darle variedad a una función que se necesita responda a diferentes cantidades y tipos de argumentos. El no tener una necesidad apropiada del mismo puede decantar en un mal uso de la funcionalidad:
```ts
    len(""); // OK
    len([0]); // OK
    len(Math.random() > 0.5 ? "hello" : [0]);
    No overload matches this call.
      Overload 1 of 2, '(s: string): number', gave the following error.
        Argument of type 'number[] | "hello"' is not assignable to parameter of type 'string'.
          Type 'number[]' is not assignable to type 'string'.
      Overload 2 of 2, '(arr: any[]): number', gave the following error.
        Argument of type 'number[] | "hello"' is not assignable to parameter of type 'any[]'.
          Type 'string' is not assignable to type 'any[]'.

    len(""); // OK
    len([0]); // OK
    len(Math.random() > 0.5 ? "hello" : [0]);
    No overload matches this call.
      Overload 1 of 2, '(s: string): number', gave the following error.
        Argument of type 'number[] | "hello"' is not assignable to parameter of type 'string'.
          Type 'number[]' is not assignable to type 'string'.
      Overload 2 of 2, '(arr: any[]): number', gave the following error.
        Argument of type 'number[] | "hello"' is not assignable to parameter of type 'any[]'.
          Type 'string' is not assignable to type 'any[]'.
```

### Declaring "this" in a Function
- Ts puede inferir la referencia de "this" en la función en la cual la estas usando.
- Ahi casos donde querremos tener mayor control de la referencia para "this" por ello, podemos definir la referencia de la cual se desprende "this".
- Esta funcion para "this" solo esta disponible para funciones declaradas, funciones tipo flecha no pueden aprovechar esta propiedad.

```ts
const user = {
  id: 123,
 
  admin: false,
  becomeAdmin: function () {
    this.admin = true;
  },
};

interface DB {
  filterUsers(filter: (this: User) => boolean): User[];
}
 
const db = getDB();
const admins = db.filterUsers(function (this: User) {
  return this.admin;
});

interface DB {
  filterUsers(filter: (this: User) => boolean): User[];
}
 
const db = getDB();
const admins = db.filterUsers(() => this.admin);
The containing arrow function captures the global value of 'this'.
Element implicitly has an 'any' type because type 'typeof globalThis' has no index signature.
```
## Other Types to Know About

### void
- Este es el retorno generado por una función que no genera un retorno, que tiene un return que no devuelve nada.
- Una función que no tiene un return podria devolver "undefined" pero esto no es lo mismo que "void"
```ts
// The inferred return type is void
function noop() {
  return;
}
```
### Object
- La explicación mas clara de este tipo es de cualquier valor que no se encuentra dentro de los primitivos, tales como "string","number",etc.
- Este es diferente de objetos vacios tales como "{ }", y diferente de el Global Type Object

### unknown
- Este tipo puede representar valores tipo "any", pero es considerado mas seguro que el mismo por el hecho que este genera errores con ts
y esto nos permite saber donde y cuando es usado.

```ts
function f1(a: any) {
  a.b(); // OK
}
function f2(a: unknown) {
  a.b();
'a' is of type 'unknown'.
}

function safeParse(s: string): unknown {
  return JSON.parse(s);
}
 
// Need to be careful with 'obj'!
const obj = safeParse(someRandomString);
```

### never
- Este tipo es visualizado cuando uan función no devuelve nada, por ejemplo detienen una ejecución o generan una observación.
```ts
function fn(x: string | number) {
  if (typeof x === "string") {
    // do something
  } else if (typeof x === "number") {
    // do something else
  } else {
    x; // has type 'never'!
  }
}
```

### Function
- Este tipo suele ser usado para describir propiedades de funciones tales como "bind", "call" and "apply"
- No es recomendable usarlo como tipo para una función anonima ya que este puede retornar any, para estos casos
 es mejor representarlos con "() => void"

 ```ts
  function doSomething(f: Function) {
  return f(1, 2, 3);
}
```

## Rest Parameters and Arguments

### Rest Parameters 
- Puedes agregar una ilimitada cantidad de parametros en una función, teniendo en cuenta ciertas condiciones:
    - Debe de ponerse este parametro al final de los demas.
    - Debes usar la sintaxis para para señalar el parametro que usaras:

```ts
function multiply(n: number, ...m: number[]) {
  return m.map((x) => n * x);
}
// 'a' gets value [10, 20, 30, 40]
const a = multiply(10, 1, 2, 3, 4);
```

### Rest Arguments
- Puedes implementar esta propiedad para juntar varios arrays y en general nos permite unirlos, pero ahi que entender bien
 lo que se quiere hacer, porque podemos incurrir en errores:

 ```ts 
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
arr1.push(...arr2);

// Inferred type is number[] -- "an array with zero or more numbers",
// not specifically two numbers
const args = [8, 5];
const angle = Math.atan2(...args);
A spread argument must either have a tuple type or be passed to a rest parameter.

// Inferred as 2-length tuple
const args = [8, 5] as const;
// OK
const angle = Math.atan2(...args);

```

## Parameter Destruturing
- Podemos usar el parametro desestruturado para ingresar una cierta cantidad de parametros, y normalmente en js no tendriamos
mas que agregarlos, pero con ts es diferente.
    - Tendremos que agregar los tipos a la hora de usarlos en la funcion.
    ```ts
    function sum({ a, b, c }) {
      console.log(a + b + c);
    }
    sum({ a: 10, b: 3, c: 9 });

    function sum({ a, b, c }: { a: number; b: number; c: number }) {
      console.log(a + b + c);
    }
    ```
    - Pero podemos implementar un Type para hacer de esto un poco mas comodo de trabajar:
    ```ts
    // Same as prior example
    type ABC = { a: number; b: number; c: number };
    function sum({ a, b, c }: ABC) {
    console.log(a + b + c);
    }
    ```

## Assignability of Functions
 
### Return type void
- Cuando asignamos a una funcion el tipado de retorno void, esta por defecto no devolvera nada.
- Incluso cuando logramos que genere un retorno diferente de void este no saldra de la funcion.

```ts
type voidFunc = () => void;
 
const f1: voidFunc = () => {
  return true;
};
 
const f2: voidFunc = () => true;
 
const f3: voidFunc = function () {
  return true;
};

const v1 = f1();
 
const v2 = f2();
 
const v3 = f3();

const src = [1, 2, 3];
const dst = [0];
 
src.forEach((el) => dst.push(el));

function f2(): void {
  // @ts-expect-error
  return true;
}
 
const f3 = function (): void {
  // @ts-expect-error
  return true;
};
```
