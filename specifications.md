# Aardvark 1.0 Specification

## Variables
Variables can be declared with `let` and given a value with `=`. Once a variable has been declared with `let`, it does not need to be re-declared. Types are optional, and, if present, go before the variable name.
Variable names CANNOT start with a number or an underscore (_). They may not include reserved symbols and may not be the same as a keyword. Variable names are case sensitive. Variables, when declared, are only accessible in the current scope and all sub-scopes.
Example:
```adk
let Number x # Declare
x = 5 # Initialize

let Number y = 5 # Declare and initialize

let z = 5 # Declare and initialize with automatic typing
```
Variables can be made static with the `static` keyword.

### Deconstruction
Aardvark supports both Array and Object deconstruction.
```adk
let [x, y, z] = [1, 2, 3]
stdout.write(x, y, z, "\n") # 1 2 3

let {a, b, c} = {a: 1, b: 2, c: 3}
stdout.write(a, b, c, "\n") # 1 2 3

let {a: p, b: q, c: r} = {a: 1, b: 2, c: 3}
stdout.write(p, q, r, "\n") # 1 2 3
```


## Comments
Single line comments in Aardvark start with `#` and end at the end of the line. Multiline comments (doc comments) begin with `#*` and end with `*#`.
Multiline comments can be embedded in many places. For example, in a function definition:
```adk
function my_function(argument1 #* Explain the argument *#, argument2 #* Explain the argument *#) {

}
```
However, this is not generally recommended because it can make the lines get quite long. Instead, use something like the following:
```adk
function my_function(
    argument1, # Explain the argument
    argument2  # Explain the argument
) {
    
}
```


## Strings
There are three types of quotes in Aardvark: single ('), double ("), and backtick (`). They all function exactly the same. All of them are multiline.

### Template Strings
A template string in Aardvark is differentiated by a leading dollar sign ($). Then, within the string, code added in curly braces will be evaluated and rendered inline. This works very similarly to Python's f-strings. Here is an example:
```adk
let name = stdin.prompt("What is your name? ")
stdout.write($"Hello, {name}!")
```

### ‼️⚠️ Escape Sequences - UNDESIGNED!!!

## Control Flow
Basic control flow in Aardvark include `if`, `while`, `for`, and `match`.

### `if`
Conditionals such as `if` are an essential to any programming language and facilitate the most basic control flow. If statements work both inline and as a block.
```adk
if condition {
    # Do something
} else if condition {
    # Do something else
} else {
    # Do something else
}
let x = y if condition else z

```
##### TODO: finish these specs

### `while`
Works like pretty much every other language. We do not have `do while` loops however.
```adk
while condition {
    # Do something
} else {
    # Exited naturally
}
```
### `for`
Works like Python.
```adk
for x in [1, 2, 3] {
    # Do something
} else {
    # Exited naturally
}
```
It also supports deconstruction and `key:value` deconstruction.
```adk
for [x, y] in [[1, 2], [3, 4]] {
    # Do something
}
for key:value in {a: 1, b: 2} {
    # Do something
}
```

### `match`
Match statements are like `if else` chains with an implied `x $=`.
Here's an example:
```adk
match value {
    case 1 {
        # This will only match the value 1.
    }
    case [1, 2] {
        # This will only match the value [1, 2].
    }
    case [1, 2, ...] {
        # This will match any array with 1 and 2 as its first two elements.
    }
    case {a: 1, b: 2} {
        # This will only match the value {a: 1, b: 2}.
    }
    case {a: 1, b: 2, ...} {
        # This will match any object with a: 1 and b: 2.
    }
    case $x {
        # This will match any value that is not one of the above.
    }
}
```
### `defer`
Defer runs the expression at the end of the function.



### Block Merging
You can merge multiple blocks.
```adk
if condition
if other condition
if yet another condition {
    # You should just use &
}

for b in a
for c in b
for d in c {
    # This can actually be useful sometimes
}
function x() while true {

}
# etc... You get the idea
```
This is how `else if` works. The else is a block that is merged with another if.


## Modules and Packages
```adk
include x, y as z
include "./x", "./y"
include y, z from x
from x include y, z
include {a: b, c} from x
include {a: b, c} from "./x"
include [x, y, z] from x
include a as b
```
Packages have an entry point file named `main.adk`.
## Operators

### Assignment
#### `=`
Assign
#### `+=`
#### `-=`
#### `*=`
#### `/=`
#### `^=`
#### `%=`
#### `?=`
#### `++`
#### `--`


### Comparison
#### `<`
Less than
#### `>`
More than
#### `<=`
Less than or equal to
#### `>=`
More than or equal to
#### `==`
Equal to
#### `!=`
Not equal to
#### `~=`
About equal to (round for Numbers, case-insensitive for Strings)
#### `@=`
Reference to
#### `in`
In
#### `$=`
`$=` is a special operator for structural pattern matching. This lets you do the same thing as is done in a `case` statement.

### Arithmetic
#### `+`
Addition
#### `-`
Subtraction
#### `*`
Multiplication
#### `/`
Division
#### `%`
Modulo
#### `^`
Exponentiation
#### `~`
Rounding???? Do we need this?


### Logical
#### `&`/`and`
#### `|`/`or`
#### `!`/`not`
#### `x|`/`xor`


### Other
#### `?`
Catches all errors about the left operand not existing or being null. If the left operand is `null` or undefined, it returns the right operand or `null`, if the right operand does not exist.
#### `@`
Makes a reference to its right operand.


## Functions
Static functions are functions that have no side-effect and will produce the same outputs for the same inputs no matter what.
How to define a function:
```adk
function my_function(argument1, argument2) {
    # Do something
}
```

You can add `?` after a parameter to make it optional. You can also give it a default value with `=`.
Deconstruction and property assignment also work in function definitions.
```adk
function my_function({a, b, c: d, e: {f: g}}, [h, i]) {
    # The arguments were deconstructed
}
class X as this {
    let a = 1
    let b = 2
    let c = 3
    $constructor(this.a, this.b, this.c) {
        # this.a, this.b, and this.c are now set.
    }
}
```
You can also specify parameter types and function return type:
```adk
function my_function(Number x, String y) -> String {
    # body
}
You can also use `...` in function parameters like JavaScript.

### Calling Functions
It works like Python. You can do keyword arguments.
```adk
my_function(x, y, z=5, a="hello")
```
### Generator Functions
Generator functions `yield` values. 
You can also use generator functions in for loops.
```adk
function my_generator() {
  yield 1
  yield 2
  let data = yield 3
  stdout.log(data);
}
let x = my_generator()
type_of(x) # Generator
x() # 1
x() # 2
x.has_ended # false
x("my data") # 3
# my data
x.has_ended # true

for x in my_generator() {
  stdout.log(x)
} # 1, 2, 3
```

### Static Functions
Static functions are equivalent to pure functions in other languages. They cannot use any global variables, have side-effects, or interact with the operating system.

### Macros
Macros are just functions that run in-place as if they are in the current scope.


## Typing
Type goes before value, C-style. Type annotations are optional.
```adk
let Number x = 5
let String y = "hello"
let [...Number] z = [1, 2, 3]
let [String, ...Number] z = ["hello", 1, 2, 3]
let [...Number, String] z = [1, 2, 3, "hello"]

let {Number x, String y} = {a: 1, b: 2}
```
Type annotations in Objects:
```adk
let a = {
    Number a: 1.
    Number b: 2.
    String c: "hello"
}
```

## Classes / Types
Classes work similar to classes in other OOP languages such as Python.
They are created with the `class` keyword.
```adk
class className as objectName {
    #* 
    NOTE: when attributes and methods are used as a class property (i.e. className.attribute), objectName will refer to the class itself, otherwise it refers to an instance of that class 
    *#
    let attribute = value # This is an attribute that the class has and that all instances of this class will start with. Static classes require all properties to be defined here.
    $constructor(...args) {
        #* 
        Called like className(...args) 
        *#
    }
    $call(...args) {
        #* 
        When an instance of this class is called. 
        return_value = objectName(...args) 
        *#
        return return_value
    }
    $delete() {
        #* 
        Called when an instance of this class is deleted. 
        delete objectName 
        *#
    }
    function method() {
        # This is a method of both the class and instances of the class.
    }
    $on_get {
        # This is called when an instance of the class is accessed.
    }
    $initializer(value) {
        # Used when the user does `let className x = value`.
    }
    $layout(x) {
        # See layouts.md
    }
    $iterate {
        # This is a generator function to yield values that can then be used in a loop.
    }
}
```

Classes can be extended off of other classes using `extends`.
```adk
class X extends Y {
    
}
```

## Arrays
Array definitions are simple. Example: `[1, 2, 3, 4]`.
Items may be different types. You can also specify types: `[Number 1, String "value", Number 9803]`.
#### array.add(item)
#### array.remove(item)
#### array.contains(item)
#### array.reverse()
#### array.filter(key)
#### array.map(key)
#### array.reduce(key)
#### array.slice(start, end, step=1)
#### array.sort(key)
#### array.length


## Objects
Kind of like JavaScript.
```adk
let x = 5
let my_object = {
    a: 1,
    b: 2,
    c: 3
}
{
    attribute: "value",
    ...my_object,
    x
}
stdout.write(my_object, "\n")
#*
{
    attribute: "value",
    a: 1,
    b: 2,
    c: 3,
    x: 5
}
*#
```

## Extending
Extending is a way to take an existing Class, Array, Set, Object, and add on to it. Let's see an example.
```
let counting = [1, 2, 3, 4]
extending counting [
  5, 6, 7, 8, 9, 10
]
stdout.write(counting) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
Extending can also be used for class extensions and function and operator overloading.

# Macros
Define a macro with the `macro` keyword. They are essentially just functions that are called in place. Here's an example:
```adk
macro define_y(value) {
    let y = value
}
define_y(5) # That code is run in-place in this scope
stdout.write(y, "\n) # 5
```