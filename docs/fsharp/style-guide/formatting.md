---
title: Instrucciones de formato de código de F#
description: 'Obtenga información sobre las directrices para dar formato a código de F #.'
ms.date: 11/04/2019
ms.openlocfilehash: a65600a6c685929aef8582e49caded6340fb09e2
ms.sourcegitcommit: 0fa2b7b658bf137e813a7f4d09589d64c148ebf5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2020
ms.locfileid: "86309708"
---
# <a name="f-code-formatting-guidelines"></a>Instrucciones de formato de código de F#

En este artículo se proporcionan instrucciones sobre cómo dar formato al código para que el código de F # sea:

* Más legible
* De acuerdo con las convenciones aplicadas por las herramientas de formato en Visual Studio y otros editores
* Similar a otro código en línea

Estas instrucciones se basan en [una guía completa de las convenciones de formato de F #](https://github.com/dungpa/fantomas/blob/master/docs/FormattingConventions.md) por [Anh-estiércol Phan](https://github.com/dungpa).

## <a name="general-rules-for-indentation"></a>Reglas generales para la sangría

F # utiliza de forma predeterminada un espacio en blanco significativo. Las instrucciones siguientes están pensadas para proporcionar orientación sobre cómo llevar a cabo algunos desafíos que esto puede imponer.

### <a name="using-spaces"></a>Usar espacios

Cuando se requiere la sangría, debe usar espacios, no pestañas. Se requiere al menos un espacio. Su organización puede crear estándares de codificación para especificar el número de espacios que se usarán para la sangría; dos, tres o cuatro espacios de sangría en cada nivel en que se produce la sangría es típico.

**Se recomiendan cuatro espacios por sangría.**

Dicho esto, la sangría de los programas es una cuestión subjetiva. Las variaciones son correctas, pero la primera regla que debe seguir es la *coherencia de la sangría*. Elija un estilo de sangría aceptado generalmente y úselo sistemáticamente en el código base.

## <a name="formatting-white-space"></a>Aplicar formato a los espacios en blanco

F # es un espacio en blanco sensible. Aunque la mayoría de las semánticas de los espacios en blanco se describen mediante una sangría adecuada, hay otros aspectos que hay que tener en cuenta.

### <a name="formatting-operators-in-arithmetic-expressions"></a>Aplicar formato a operadores en expresiones aritméticas

Use siempre el espacio en blanco alrededor de las expresiones aritméticas binarias:

```fsharp
let subtractThenAdd x = x - 1 + 3
```

`-`Los operadores unarios siempre deben ir seguidos inmediatamente del valor que están negando:

```fsharp
// OK
let negate x = -x

// Bad
let negateBad x = - x
```

Agregar un carácter de espacio en blanco después del `-` operador puede provocar confusión en otros.

En Resumen, es importante que siempre:

* Operadores binarios de envolvente con espacio en blanco
* Nunca debe haber un espacio en blanco al final después de un operador unario

La instrucción del operador aritmético binario es especialmente importante. Si no se rodea un operador binario `-` , cuando se combina con determinadas opciones de formato, podría interpretarlo como unario `-` .

### <a name="surround-a-custom-operator-definition-with-white-space"></a>Envolver una definición de operador personalizado con espacio en blanco

Use siempre el espacio en blanco para rodear una definición de operador:

```fsharp
// OK
let ( !> ) x f = f x

// Bad
let (!>) x f = f x
```

Para cualquier operador personalizado que empiece por `*` y que tenga más de un carácter, debe agregar un espacio en blanco al principio de la definición para evitar la ambigüedad del compilador. Por este motivo, se recomienda que solo incluya las definiciones de todos los operadores con un solo carácter de espacio en blanco.

### <a name="surround-function-parameter-arrows-with-white-space"></a>Flechas de parámetros de función envolvente con espacio en blanco

Al definir la firma de una función, use el espacio en blanco que rodea el `->` símbolo:

```fsharp
// OK
type MyFun = int -> int -> string

// Bad
type MyFunBad = int->int->string
```

### <a name="surround-function-arguments-with-white-space"></a>Rodear argumentos de función con espacio en blanco

Al definir una función, use el espacio en blanco alrededor de cada argumento.

```fsharp
// OK
let myFun (a: decimal) b c = a + b + c

// Bad
let myFunBad (a:decimal)(b)c = a + b + c
```

### <a name="place-parameters-on-a-new-line-for-long-member-definitions"></a>Colocar parámetros en una nueva línea para definiciones de miembros largas

Si tiene una definición de miembro muy larga, coloque los parámetros en nuevas líneas y aplíqueles sangría para que coincidan con el nivel de sangría del parámetro subsiguiente.

```fsharp
type C() =
    member _.LongMethodWithLotsOfParameters(aVeryLongType: AVeryLongTypeThatYouNeedToUse,
                                            aSecondVeryLongType: AVeryLongTypeThatYouNeedToUse,
                                            aThirdVeryLongType: AVeryLongTypeThatYouNeedToUse) =
        // ... the body of the method follows
```

Esto también se aplica a los constructores:

```fsharp
type C(aVeryLongType: AVeryLongTypeThatYouNeedToUse,
       aSecondVeryLongType: AVeryLongTypeThatYouNeedToUse,
       aThirdVeryLongType: AVeryLongTypeThatYouNeedToUse) =
    // ... the body of the class follows
```

Si hay una anotación de tipo de valor devuelto explícita, puede estar al final de `)` y antes de `=` , o en una línea nueva. Si el tipo de valor devuelto también tiene un nombre largo, el último podría ser preferible:

```fsharp
type C() =
    member _.LongMethodWithLotsOfParameters(aVeryLongType: AVeryLongTypeThatYouNeedToUse,
                                            aSecondVeryLongType: AVeryLongTypeThatYouNeedToUse,
                                            aThirdVeryLongType: AVeryLongTypeThatYouNeedToUse)
                                            : AVeryLongReturnType =
        // ... the body of the method follows
```

### <a name="type-annotations"></a>Anotaciones de tipo

#### <a name="right-pad-function-argument-type-annotations"></a>Anotaciones del tipo de argumento de la función del botón secundario

Al definir argumentos con anotaciones de tipo, use el espacio en blanco después del `:` símbolo:

```fsharp
// OK
let complexFunction (a: int) (b: int) c = a + b + c

// Bad
let complexFunctionBad (a :int) (b :int) (c:int) = a + b + c
```

#### <a name="surround-return-type-annotations-with-white-space"></a>Anotaciones de tipo de valor devuelto envolvente con espacio en blanco

En una anotación de tipo de valor o función enlazada a (tipo de valor devuelto en el caso de una función), use el espacio en blanco antes y después del `:` símbolo:

```fsharp
// OK
let expensiveToCompute : int = 0 // Type annotation for let-bound value
let myFun (a: decimal) b c : decimal = a + b + c // Type annotation for the return type of a function
// Bad
let expensiveToComputeBad1:int = 1
let expensiveToComputeBad2 :int = 2
let myFunBad (a: decimal) b c:decimal = a + b + c
```

## <a name="formatting-blank-lines"></a>Aplicar formato a líneas en blanco

* Separe las definiciones de clase y de función de nivel superior con dos líneas en blanco.
* Las definiciones de método dentro de una clase se separan mediante una sola línea en blanco.
* Se pueden usar líneas en blanco adicionales (moderadamente) para separar grupos de funciones relacionadas. Es posible que se omitan líneas en blanco entre un grupo de una sola línea relacionada (por ejemplo, un conjunto de implementaciones ficticias).
* Use líneas en blanco en las funciones, con moderación, para indicar secciones lógicas.

## <a name="formatting-comments"></a>Aplicar formato a comentarios

Normalmente, se prefieren varios comentarios de barra diagonal doble sobre los comentarios de bloque de estilo ML.

```fsharp
// Prefer this style of comments when you want
// to express written ideas on multiple lines.

(*
    ML-style comments are fine, but not a .NET-ism.
    They are useful when needing to modify multi-line comments, though.
*)
```

Los comentarios en línea deben poner en mayúscula la primera letra.

```fsharp
let f x = x + 1 // Increment by one.
```

## <a name="naming-conventions"></a>Convenciones de nomenclatura

### <a name="use-camelcase-for-class-bound-expression-bound-and-pattern-bound-values-and-functions"></a>Usar camelCase para funciones y valores enlazados a expresiones y enlazados a un patrón

Es común y acepta el estilo F # para usar camelCase para todos los nombres enlazados como variables locales o en coincidencias de patrones y definiciones de función.

```fsharp
// OK
let addIAndJ i j = i + j

// Bad
let addIAndJ I J = I+J

// Bad
let AddIAndJ i j = i + j
```

Las funciones enlazadas localmente en clases también deben usar camelCase.

```fsharp
type MyClass() =

    let doSomething () =

    let firstResult = ...

    let secondResult = ...

    member x.Result = doSomething()
```

### <a name="use-camelcase-for-module-bound-public-functions"></a>Usar camelCase para funciones públicas enlazadas a módulos

Cuando una función enlazada a un módulo forma parte de una API pública, debe usar camelCase:

```fsharp
module MyAPI =
    let publicFunctionOne param1 param2 param2 = ...

    let publicFunctionTwo param1 param2 param3 = ...
```

### <a name="use-camelcase-for-internal-and-private-module-bound-values-and-functions"></a>Usar camelCase para funciones y valores enlazados a módulos internos y privados

Use camelCase para valores enlazados a módulos privados, incluidos los siguientes:

* Funciones ad hoc en scripts

* Valores que conforman la implementación interna de un módulo o tipo

```fsharp
let emailMyBossTheLatestResults =
    ...
```

### <a name="use-camelcase-for-parameters"></a>Usar camelCase para los parámetros

Todos los parámetros deben usar camelCase de acuerdo con las convenciones de nomenclatura de .NET.

```fsharp
module MyModule =
    let myFunction paramOne paramTwo = ...

type MyClass() =
    member this.MyMethod(paramOne, paramTwo) = ...
```

### <a name="use-pascalcase-for-modules"></a>Uso de PascalCase para módulos

Todos los módulos (de nivel superior, interno, privado, anidado) deben usar PascalCase.

```fsharp
module MyTopLevelModule

module Helpers =
    module private SuperHelpers =
        ...

    ...
```

### <a name="use-pascalcase-for-type-declarations-members-and-labels"></a>Usar PascalCase para las declaraciones de tipos, los miembros y las etiquetas

Todas las clases, interfaces, estructuras, enumeraciones, delegados, registros y uniones discriminadas deben llamarse con PascalCase. Los miembros de tipos y etiquetas para registros y uniones discriminadas también deben usar PascalCase.

```fsharp
type IMyInterface =
    abstract Something: int

type MyClass() =
    member this.MyMethod(x, y) = x + y

type MyRecord = { IntVal: int; StringVal: string }

type SchoolPerson =
    | Professor
    | Student
    | Advisor
    | Administrator
```

### <a name="use-pascalcase-for-constructs-intrinsic-to-net"></a>Uso de PascalCase para construcciones intrínsecas de .NET

Los espacios de nombres, excepciones, eventos y proyectos/ `.dll` nombres también deben usar PascalCase. Esto no solo hace que el consumo de otros lenguajes .NET parezca más natural a los consumidores, sino que también es coherente con las convenciones de nomenclatura de .NET que es probable que encuentre.

### <a name="avoid-underscores-in-names"></a>Evitar el carácter de subrayado en los nombres

Históricamente, algunas bibliotecas de F # usaban guiones bajos en los nombres. Sin embargo, esto ya no se acepta ampliamente, en parte porque entra en conflicto con las convenciones de nomenclatura de .NET. Dicho esto, algunos programadores de F # usan subrayados en gran medida, en parte por motivos históricos, y la tolerancia y el respeto son importantes. Sin embargo, tenga en cuenta que el estilo suele estar deshabilitado por otros usuarios que tienen la opción de usarlos.

Una excepción incluye la interoperabilidad con componentes nativos, donde los guiones bajos son comunes.

### <a name="use-standard-f-operators"></a>Usar operadores estándar de F #

Los operadores siguientes se definen en la biblioteca estándar de F # y deben usarse en lugar de definir equivalentes. Se recomienda usar estos operadores, ya que tiende a hacer que el código sea más legible y idiomático. Los desarrolladores con un fondo en OCaml u otro lenguaje de programación funcional pueden estar acostumbrados a diferentes expresiones. En la lista siguiente se resumen los operadores de F # recomendados.

```fsharp
x |> f // Forward pipeline
f >> g // Forward composition
x |> ignore // Discard away a value
x + y // Overloaded addition (including string concatenation)
x - y // Overloaded subtraction
x * y // Overloaded multiplication
x / y // Overloaded division
x % y // Overloaded modulus
x && y // Lazy/short-cut "and"
x || y // Lazy/short-cut "or"
x <<< y // Bitwise left shift
x >>> y // Bitwise right shift
x ||| y // Bitwise or, also for working with “flags” enumeration
x &&& y // Bitwise and, also for working with “flags” enumeration
x ^^^ y // Bitwise xor, also for working with “flags” enumeration
```

### <a name="use-prefix-syntax-for-generics-foot-in-preference-to-postfix-syntax-t-foo"></a>Use la sintaxis de prefijo para genéricos ( `Foo<T>` ) en preferencia a la sintaxis de postfijo ( `T Foo` )

F # hereda el estilo de ambos postfijos de los tipos genéricos de nomenclatura (por ejemplo,), así `int list` como el estilo de .net de prefijo (por ejemplo, `list<int>` ). Prefiera el estilo .NET, excepto para cinco tipos específicos:

1. En el caso de las listas de F #, use el formato de postfijo: `int list` en lugar de `list<int>` .
2. En el caso de las opciones de F #, use el formato de postfijo: `int option` en lugar de `option<int>` .
3. Para las opciones de valor de F #, use el formato de postfijo: `int voption` en lugar de `voption<int>` .
4. En el caso de las matrices de F #, use el nombre sintáctico `int[]` en lugar de `int array` o `array<int>` .
5. En el caso de las celdas de referencia, use `int ref` en lugar de `ref<int>` o `Ref<int>` .

En el caso de todos los demás tipos, use el formato de prefijo.

## <a name="formatting-tuples"></a>Dar formato a tuplas

Una creación de instancias de tupla debe ir entre paréntesis y las comas delimitadoras deben ir seguidas de un solo espacio, por ejemplo: `(1, 2)` , `(x, y, z)` .

Normalmente se acepta para omitir paréntesis en la coincidencia de patrones de tuplas:

```fsharp
let (x, y) = z // Destructuring
let x, y = z // OK

// OK
match x, y with
| 1, _ -> 0
| x, 1 -> 0
| x, y -> 1
```

También se acepta normalmente para omitir los paréntesis si la tupla es el valor devuelto de una función:

```fsharp
// OK
let update model msg =
    match msg with
    | 1 -> model + 1, []
    | _ -> model, [ msg ]
```

En Resumen, se prefieren las instancias de tupla entre paréntesis, pero cuando se usan tuplas para la coincidencia de patrones o un valor devuelto, se considera adecuado para evitar paréntesis.

## <a name="formatting-discriminated-union-declarations"></a>Dar formato a las declaraciones de Unión discriminadas

Aplicar sangría `|` en la definición de tipo en cuatro espacios:

```fsharp
// OK
type Volume =
    | Liter of float
    | FluidOunce of float
    | ImperialPint of float

// Not OK
type Volume =
| Liter of float
| USPint of float
| ImperialPint of float
```

## <a name="formatting-discriminated-unions"></a>Aplicar formato a uniones discriminadas

Las uniones discriminadas con instancias que se dividen entre varias líneas deben proporcionar a los datos contenidos un nuevo ámbito con sangría:

```fsharp
let tree1 =
    BinaryNode
        (BinaryNode(BinaryValue 1, BinaryValue 2),
         BinaryNode(BinaryValue 3, BinaryValue 4))
```

El paréntesis de cierre también puede estar en una nueva línea:

```fsharp
let tree1 =
    BinaryNode(
        BinaryNode(BinaryValue 1, BinaryValue 2),
        BinaryNode(BinaryValue 3, BinaryValue 4)
    )
```

## <a name="formatting-record-declarations"></a>Dar formato a declaraciones de registro

Aplicar sangría `{` en la definición de tipo en cuatro espacios e iniciar la lista de campos en la misma línea:

```fsharp
// OK
type PostalAddress =
    { Address: string
      City: string
      Zip: string }
    member x.ZipAndCity = sprintf "%s %s" x.Zip x.City

// Not OK
type PostalAddress =
  { Address: string
    City: string
    Zip: string }
    member x.ZipAndCity = sprintf "%s %s" x.Zip x.City

// Unusual in F#
type PostalAddress =
    {
        Address: string
        City: string
        Zip: string
    }
```

Es preferible colocar el token de apertura en una nueva línea y el token de cierre en una nueva línea si se declaran implementaciones de interfaz o miembros en el registro:

```fsharp
// Declaring additional members on PostalAddress
type PostalAddress =
    {
        Address: string
        City: string
        Zip: string
    }
    member x.ZipAndCity = sprintf "%s %s" x.Zip x.City

type MyRecord =
    {
        SomeField: int
    }
    interface IMyInterface
```

## <a name="formatting-records"></a>Aplicar formato a registros

Los registros cortos se pueden escribir en una línea:

```fsharp
let point = { X = 1.0; Y = 0.0 }
```

Los registros que son más largas deben usar nuevas líneas para las etiquetas:

```fsharp
let rainbow =
    { Boss = "Jeffrey"
      Lackeys = ["Zippy"; "George"; "Bungle"] }
```

Es preferible colocar el token de apertura en una nueva línea, el contenido con pestañas en un ámbito y el token de cierre en una nueva línea si:

* Mover registros en el código con diferentes ámbitos de sangría
* Canalizarlos en una función

```fsharp
let rainbow =
    {
        Boss1 = "Jeffrey"
        Boss2 = "Jeffrey"
        Boss3 = "Jeffrey"
        Boss4 = "Jeffrey"
        Boss5 = "Jeffrey"
        Boss6 = "Jeffrey"
        Boss7 = "Jeffrey"
        Boss8 = "Jeffrey"
        Lackeys = ["Zippy"; "George"; "Bungle"]
    }

type MyRecord =
    {
        SomeField: int
    }
    interface IMyInterface

let foo a =
    a
    |> Option.map (fun x ->
        {
            MyField = x
        })
```

Las mismas reglas se aplican a los elementos de lista y matriz.

## <a name="formatting-copy-and-update-record-expressions"></a>Dar formato a expresiones de registro de copia y actualización

Una expresión de registro de copia y actualización sigue siendo un registro, por lo que se aplican instrucciones similares.

Las expresiones cortas pueden caber en una línea:

```fsharp
let point2 = { point with X = 1; Y = 2 }
```

Las expresiones más largas deben usar nuevas líneas:

```fsharp
let rainbow2 =
    { rainbow with
        Boss = "Jeffrey"
        Lackeys = [ "Zippy"; "George"; "Bungle" ] }
```

Y, al igual que con la guía de registro, puede que desee dedicar líneas independientes a las llaves y aplicar sangría a un ámbito a la derecha con la expresión. En algunos casos especiales, como el ajuste de un valor con un opcional sin paréntesis, puede que tenga que mantener una llave en una línea:

```fsharp
type S = { F1: int; F2: string }
type State = { F:  S option }

let state = { F = Some { F1 = 1; F2 = "Hello" } }
let newState =
    {
        state with
            F = Some {
                    F1 = 0
                    F2 = ""
                }
    }
```

## <a name="formatting-lists-and-arrays"></a>Aplicar formato a listas y matrices

Escribe `x :: l` espacios alrededor del `::` operador ( `::` es un operador infijo, por lo que está rodeado por espacios).

La lista y las matrices declaradas en una sola línea deben tener un espacio después del corchete de apertura y antes del corchete de cierre:

```fsharp
let xs = [ 1; 2; 3 ]
let ys = [| 1; 2; 3; |]
```

Utilice siempre al menos un espacio entre dos operadores distintivos de tipo llave. Por ejemplo, deje un espacio entre `[` y `{` .

```fsharp
// OK
[ { IngredientName = "Green beans"; Quantity = 250 }
  { IngredientName = "Pine nuts"; Quantity = 250 }
  { IngredientName = "Feta cheese"; Quantity = 250 }
  { IngredientName = "Olive oil"; Quantity = 10 }
  { IngredientName = "Lemon"; Quantity = 1 } ]

// Not OK
[{ IngredientName = "Green beans"; Quantity = 250 }
 { IngredientName = "Pine nuts"; Quantity = 250 }
 { IngredientName = "Feta cheese"; Quantity = 250 }
 { IngredientName = "Olive oil"; Quantity = 10 }
 { IngredientName = "Lemon"; Quantity = 1 }]
```

La misma instrucción se aplica a las listas o matrices de tuplas.

Las listas y matrices que se dividen entre varias líneas siguen una regla similar a la de los registros:

```fsharp
let pascalsTriangle =
    [|
        [| 1 |]
        [| 1; 1 |]
        [| 1; 2; 1 |]
        [| 1; 3; 3; 1 |]
        [| 1; 4; 6; 4; 1 |]
        [| 1; 5; 10; 10; 5; 1 |]
        [| 1; 6; 15; 20; 15; 6; 1 |]
        [| 1; 7; 21; 35; 35; 21; 7; 1 |]
        [| 1; 8; 28; 56; 70; 56; 28; 8; 1 |]
    |]
```

Y como con los registros, la declaración de los corchetes de apertura y cierre en su propia línea hará que el código y la canalización en funciones sean más fáciles.

Al generar matrices y listas mediante programación, `->` es preferible `do ... yield` cuando se genera siempre un valor:

```fsharp
// Preferred
let squares = [ for x in 1..10 -> x * x ]

// Not preferred
let squares' = [ for x in 1..10 do yield x * x ]
```

Las versiones anteriores del lenguaje F # requerían especificar en situaciones en las que los `yield` datos se pueden generar de forma condicional, o puede haber expresiones consecutivas que se van a evaluar. Prefiera omitir estas `yield` palabras clave a menos que deba compilar con una versión anterior del lenguaje F #:

```fsharp
// Preferred
let daysOfWeek includeWeekend =
    [
        "Monday"
        "Tuesday"
        "Wednesday"
        "Thursday"
        "Friday"
        if includeWeekend then
            "Saturday"
            "Sunday"
    ]

// Not preferred
let daysOfWeek' includeWeekend =
    [
        yield "Monday"
        yield "Tuesday"
        yield "Wednesday"
        yield "Thursday"
        yield "Friday"
        if includeWeekend then
            yield "Saturday"
            yield "Sunday"
    ]
```

En algunos casos, `do...yield` puede ayudar a mejorar la legibilidad. Estos casos, aunque subjetiva, deben tenerse en cuenta.

## <a name="formatting-if-expressions"></a>Aplicar formato a expresiones if

La sangría de los condicionales depende del tamaño de las expresiones que los componen. Si `cond` `e1` y `e2` son cortos, simplemente escríbalos en una línea:

```fsharp
if cond then e1 else e2
```

Si `cond` , `e1` o `e2` son más largas, pero no varias líneas:

```fsharp
if cond
then e1
else e2
```

Si alguna de las expresiones es de varias líneas:

```fsharp
if cond then
    e1
else
    e2
```

A varios condicionales con `elif` y `else` se les aplica una sangría en el mismo ámbito que el `if` :

```fsharp
if cond1 then e1
elif cond2 then e2
elif cond3 then e3
else e4
```

### <a name="pattern-matching-constructs"></a>Construcciones de coincidencia de patrones

Use una `|` cláusula for each de una coincidencia sin sangría. Si la expresión es breve, puede considerar el uso de una sola línea si cada subexpresión también es simple.

```fsharp
// OK
match l with
| { him = x; her = "Posh" } :: tail -> x
| _ :: tail -> findDavid tail
| [] -> failwith "Couldn't find David"

// Not OK
match l with
    | { him = x; her = "Posh" } :: tail -> x
    | _ :: tail -> findDavid tail
    | [] -> failwith "Couldn't find David"
```

Si la expresión de la derecha de la flecha de coincidencia de patrones es demasiado grande, muévala a la línea siguiente, con una sangría a un paso de `match` / `|` .

```fsharp
match lam with
| Var v -> 1
| Abs(x, body) ->
    1 + sizeLambda body
| App(lam1, lam2) ->
    sizeLambda lam1 + sizeLambda lam2

```

La coincidencia de patrones de funciones anónimas, a partir de `function` , no suele ser una sangría demasiado lejana. Por ejemplo, la sangría de un ámbito es la siguiente:

```fsharp
lambdaList
|> List.map (function
    | Abs(x, body) -> 1 + sizeLambda 0 body
    | App(lam1, lam2) -> sizeLambda (sizeLambda 0 lam1) lam2
    | Var v -> 1)
```

La coincidencia de patrones en funciones definidas por `let` o `let rec` debe tener una sangría de cuatro espacios después de iniciarse `let` , incluso si `function` se usa la palabra clave:

```fsharp
let rec sizeLambda acc = function
    | Abs(x, body) -> sizeLambda (succ acc) body
    | App(lam1, lam2) -> sizeLambda (sizeLambda acc lam1) lam2
    | Var v -> succ acc
```

No se recomienda alinear las flechas.

## <a name="formatting-trywith-expressions"></a>Aplicar formato a expresiones try/with

Se debe aplicar sangría a la coincidencia de patrones en el tipo de excepción en el mismo nivel que `with` .

```fsharp
try
    if System.DateTime.Now.Second % 3 = 0 then
        raise (new System.Exception())
    else
        raise (new System.ApplicationException())
with
| :? System.ApplicationException ->
    printfn "A second that was not a multiple of 3"
| _ ->
    printfn "A second that was a multiple of 3"
```

## <a name="formatting-function-parameter-application"></a>Aplicación de formato de parámetros de función

En general, la mayoría de las aplicaciones de parámetros de función se realizan en la misma línea.

Si desea aplicar parámetros a una función en una nueva línea, aplíqueles sangría en un ámbito.

```fsharp
// OK
sprintf "\t%s - %i\n\r"
     x.IngredientName x.Quantity

// OK
sprintf
     "\t%s - %i\n\r"
     x.IngredientName x.Quantity

// OK
let printVolumes x =
    printf "Volume in liters = %f, in us pints = %f, in imperial = %f"
        (convertVolumeToLiter x)
        (convertVolumeUSPint x)
        (convertVolumeImperialPint x)
```

Las mismas directrices se aplican a las expresiones lambda como argumentos de función. Si el cuerpo de una expresión lambda, el cuerpo puede tener otra línea, con sangría en un ámbito

```fsharp
let printListWithOffset a list1 =
    List.iter
        (fun elem -> printfn "%d" (a + elem))
        list1

// OK if lambda body is long enough
let printListWithOffset a list1 =
    List.iter
        (fun elem ->
            printfn "%d" (a + elem))
        list1
```

Sin embargo, si el cuerpo de una expresión lambda tiene más de una línea, considere la posibilidad de factorizarla en una función independiente en lugar de tener una construcción de varias líneas aplicada como un solo argumento a una función.

### <a name="formatting-infix-operators"></a>Aplicar formato a los operadores de infijo

Operadores independientes por espacios. Las excepciones obvias a esta regla son los `!` `.` operadores y.

Las expresiones infijas son correctas para la misma columna:

```fsharp
acc +
(sprintf "\t%s - %i\n\r"
     x.IngredientName x.Quantity)

let function1 arg1 arg2 arg3 arg4 =
    arg1 + arg2 +
    arg3 + arg4
```

### <a name="formatting-pipeline-operators"></a>Operadores de canalización de formato

`|>`Los operadores de canalización deben ir debajo de las expresiones en las que operan.

```fsharp
// Preferred approach
let methods2 =
    System.AppDomain.CurrentDomain.GetAssemblies()
    |> List.ofArray
    |> List.map (fun assm -> assm.GetTypes())
    |> Array.concat
    |> List.ofArray
    |> List.map (fun t -> t.GetMethods())
    |> Array.concat

// Not OK
let methods2 = System.AppDomain.CurrentDomain.GetAssemblies()
            |> List.ofArray
            |> List.map (fun assm -> assm.GetTypes())
            |> Array.concat
            |> List.ofArray
            |> List.map (fun t -> t.GetMethods())
            |> Array.concat
```

### <a name="formatting-modules"></a>Módulos de formato

Se debe aplicar sangría al código de un módulo local en relación con el módulo, pero no se debe aplicar sangría al código de un módulo de nivel superior. No es necesario aplicar sangría a los elementos de espacio de nombres.

```fsharp
// A is a top-level module.
module A

let function1 a b = a - b * b
```

```fsharp
// A1 and A2 are local modules.
module A1 =
    let function1 a b = a * a + b * b

module A2 =
    let function2 a b = a * a - b * b
```

### <a name="formatting-object-expressions-and-interfaces"></a>Dar formato a expresiones e interfaces de objeto

Las interfaces y las expresiones de objeto se deben alinear de la misma manera con `member` una sangría después de cuatro espacios.

```fsharp
let comparer =
    { new IComparer<string> with
          member x.Compare(s1, s2) =
              let rev (s: String) =
                  new String (Array.rev (s.ToCharArray()))
              let reversed = rev s1
              reversed.CompareTo (rev s2) }
```

### <a name="formatting-white-space-in-expressions"></a>Aplicar formato a los espacios en blanco en expresiones

Evite el espacio en blanco extraño en las expresiones de F #.

```fsharp
// OK
spam (ham.[1])

// Not OK
spam ( ham.[ 1 ] )
```

Los argumentos con nombre tampoco deben tener espacio alrededor del `=` :

```fsharp
// OK
let makeStreamReader x = new System.IO.StreamReader(path=x)

// Not OK
let makeStreamReader x = new System.IO.StreamReader(path = x)
```

## <a name="formatting-attributes"></a>Aplicar formato a atributos

[Los atributos](../language-reference/attributes.md) se colocan sobre una construcción:

```fsharp
[<SomeAttribute>]
type MyClass() = ...

[<RequireQualifiedAccess>]
module M =
    let f x = x

[<Struct>]
type MyRecord =
    { Label1: int
      Label2: string }
```

### <a name="formatting-attributes-on-parameters"></a>Aplicar formato a atributos en parámetros

Los atributos también se pueden colocar en parámetros. En este caso, coloque entonces en la misma línea que el parámetro y antes del nombre:

```fsharp
// Defines a class that takes an optional value as input defaulting to false.
type C() =
    member _.M([<Optional; DefaultParameterValue(false)>] doSomething: bool)
```

### <a name="formatting-multiple-attributes"></a>Aplicar formato a varios atributos

Cuando se aplican varios atributos a una construcción que no es un parámetro, deben colocarse de forma que haya un atributo por línea:

```fsharp
[<Struct>]
[<IsByRefLike>]
type MyRecord =
    { Label1: int
      Label2: string }
```

Cuando se aplica a un parámetro, deben estar en la misma línea y estar separados por un `;` separador.

## <a name="formatting-literals"></a>Aplicar formato a literales

Los [literales de F #](../language-reference/literals.md) que usan el `Literal` atributo deben colocar el atributo en su propia línea y usar PascalCase naming:

```fsharp
[<Literal>]
let Path = __SOURCE_DIRECTORY__ + "/" + __SOURCE_FILE__

[<Literal>]
let MyUrl = "www.mywebsitethatiamworkingwith.com"
```

Evite colocar el atributo en la misma línea que el valor.
