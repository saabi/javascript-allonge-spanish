# The Recipe Cheat Sheet

En las recetas, puede que veas una o más de las siguientes construcciones siendo usadas antes de ser completamente explicadas en el texto. Aquí hay algunas explicaciones breves para sacarte del apuro:

### apply y call

Las funciones son llamadas con `()`. Pero también tienen *métodos* que permiten llamarlas con argumentos. `.call` y `.apply` van a ser explicadas cuando hablemos de [contextos de funciones](#context), pero aquí hay algunos ejemplos:

    function plus (a, b) {
      return a + b
    }

    plus(2, 3)
      //=> 5

    plus.call(this, 2, 3)
      //=> 5

    plus.apply(this, [2, 3])
      //=> 5

### slice

Los arreglos tienen un método `.slice`. La función siempre puede ser encontrada en `Array.prototype.slice`. Funciona de la siguiente manera:

    [1, 2, 3, 4, 5].slice(0)
      //=> [1, 2, 3, 4, 5]

    [1, 2, 3, 4, 5].slice(1)
      //=> [2, 3, 4, 5]

    [1, 2, 3, 4, 5].slice(1, 4)
      //=> [2, 3, 4]

Date cuenta de que `slice` siempre crea un nuevo arreglo, de manera que `.slice(0)` hace una copia del arreglo. La pseudo-variable [arguments](#arguments-again) no es un arreglo, pero puedes usar `.slice` para obtener todos o parte de los argumentos en un arreglo:

    Array.prototype.slice.call(arguments, 0)
      //=> returns the arguments in an array.

    function butFirst () {
      return Array.prototype.slice.call(arguments, 1)
    }

    butFirst('a', 'b', 'c', 'd')
      //=> [ 'b', 'c', 'd' ]

Por simplicidad y una pequeña mejora de rapidez, `slice` usualmente es enlazado a una variable local:

    var __slice = Array.prototype.slice;

    function butFirst () {
      return __slice.call(arguments, 1)
    }

O incluso:

    var __slice = Array.prototype.slice;

    function slice (list, from, to) {
      return __slice.call(list, from, to)
    }

    function butFirst () {
      return slice(arguments, 1)
    }

### concat

Los arreglos cuentan con otro método útil, `.concat`. Concat devuelve un arreglo creado por la concatenación del receptor con su argumento:

    [1, 2, 3].concat([2, 1])
      //=> [1, 2, 3, 2, 1]

### Propiedad length de una Función

Las funciones tienen una propiedad `.length` que cuenta el número de argumentos declarado:

    function (a, b, c) { return a + b + c }.length
      //=> 3