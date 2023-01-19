# Homework JavaScript Avanzado I

## Scope & Hoisting

Determiná que será impreso en la consola, sin ejecutar el código.

> Investiga cuál es la diferencia entre declarar una variable con `var` y directamente asignarle un valor.

```javascript
//console.log(x) = 10
//console.log(a) = 8
//console.log(b) = 8
//console.log(b) = 9
//console.log(b) = 10
//console.log(x) = 1

x = 1; //declara que 10 es igual a 1
var a = 5; //declara las variables
var b = 10;
var c = function (a, b, c) { //declara la var c como una funcion
   var x = 10;
   console.log(x);
   console.log(a);
   var f = function (a, b, c) {
      b = a;
      console.log(b);
      b = c;
      var x = 5;
   };
   f(a, b, c);
   console.log(b);
};
c(8, 9, 10);
console.log(b);
console.log(x);

```

```javascript
//undefined
console.log(bar);
console.log(baz);
foo();
function foo() {
   console.log('Hola!');
}
var bar = 1;
baz = 2;
```

```javascript
//Franco
//undefined
var instructor = 'Tony';
if (true) {
   var instructor = 'Franco';
}
console.log(instructor);

```

```javascript
//Tony
//Franco
//Tony
var instructor = 'Tony';
console.log(instructor);
(function () {
   if (true) {
      var instructor = 'Franco';
      console.log(instructor);
   }
})(); //ejecuta la funcion
console.log(instructor);
```

```javascript
//The flash
//Reserver Flash
//The Flash
//Franco
//undefined
var instructor = 'Tony'; 
let pm = 'Franco';
if (true) {
   var instructor = 'The Flash';
   let pm = 'Reverse Flash';
   console.log(instructor);
   console.log(pm);
}
console.log(instructor);
console.log(pm);
```

### Coerción de Datos

¿Cuál crees que será el resultado de la ejecución de estas operaciones?:

```javascript
//divide ambos numeros//
6 / "3"
//multiplica ambos numeros//
"2" * "3"
//suma los numeros y al resultado les suma el string//
4 + 5 + "px"
//coloca el string y pasa a los numeros a string $45//
"$" + 4 + 5
//Resta//
"4" - 2
//retorna NaN no soy un numero//
"4px" - 2
//Infinity en JavaScript es un número especial con una propiedad interesante: es más grande que cualquier número infinito//
7 / 0
//quita las llaves y deja el 0 en el array//
{}[0]
//devuelve 9 pasrseInt comprueba el argumento e intenta devolver un entero
parseInt("09")
//devuelve el ultimo numero, evalua que los dos valores sean true (utiliza AND)
5 && 2
2 && 5
//devuelve el numero mas grande (busca el valor que es true y lo devuelve, al evaluar el primero cumple las condiciones y lo retorna)
5 || 0
0 || 5 // 0 siempre se traduce como false, entonces evalua el siguiente y lo retorna
[3]+[3]-[10]
//retorna false debido a que 1 es falso
3>2>1
[] == ![] //da True, porque java, al tomarlo como objeto, y al no estar declarado y vacio, lo lleva a un dato nativo, en este caso un string vacio, lo lleva a continuacion a un falsy que es igual a 0, entonces compara que ambos dan 0 y al preguntar si son iguales, retorna true
```

> Si te quedó alguna duda repasá con [este artículo](http://javascript.info/tutorial/object-conversion).

### Hoisting

¿Cuál es el output o salida en consola luego de ejecutar este código? Explicar por qué:
//retorna 2 debido a que esta ejecutando la funcion foo
```javascript
function test() {
   console.log(a); //undefined debido a que ejecuta la variable A antes de declararla
   console.log(foo()); //ejecuta la funcion y retorna 2 

   var a = 1;
   function foo() { 
      return 2;
   }
}

test();
```

Y el de este código? :

```javascript
//undefined 
var snack = 'Meow Mix';

function getFood(food) { //Hosting sube la variable porque si da true la va a necesitar, por lo tanto la crea dentro de la funcion
   if (food) {
      var snack = 'Friskies';
      return snack;
   }
   return snack;
}

getFood(false);
```

### This

¿Cuál es el output o salida en consola luego de ejecutar esté código? Explicar por qué:

```javascript
var fullname = 'Juan Perez';
var obj = {
   fullname: 'Natalia Nerea',
   prop: {
      fullname: 'Aurelio De Rosa',
      getFullname: function () {
         return this.fullname;
      },
   },
};

console.log(obj.prop.getFullname()); //retorna aurelio porque el this.fullname esta dentro del metodo getFullname que esta dentro del objeto prop

var test = obj.prop.getFullname;

console.log(test());
```

### Event loop

Considerando el siguiente código, ¿Cuál sería el orden en el que se muestra por consola? ¿Por qué?
1, 4, 3, 2 debido a que se utiliza funciones que se ejecutan en orden, esta es una funcion asincronica, porque se agregan a una cola, que ejecuta luego de terminar una tarea indicada antes. 
```javascript
function printing() {
   console.log(1);
   setTimeout(function () {
      console.log(2);
   }, 1000);
   setTimeout(function () {
      console.log(3);
   }, 0);
   console.log(4);
}

printing();
```
