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

```
##### TODO: finish these specs

### `while`

### `for`

### `match`


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
include x, y
include "./x", "./y"
include y, z from x
from x include y, z
include {a: b, c} from x
include {a: b, c} from "./x"
```
Packages have an entry point file named `main.py`.
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
TODO
    
## Typing
Type goes before value, C-style

## Classes / Types
Classes work similar to classes in other OOP languages such as Python.
They are created with the `class` keyword.

## Arrays
TODO

## Objects
Like JavaScript.

## Extending
Extending is a way to take an existing Class, Array, Set, Object, and add on to it. Let's see an example.
```
let counting = [1, 2, 3, 4]
extending counting [
  5, 6, 7, 8, 9, 10
]
stdout.write(counting) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
Extending can also be used for function and operator overloading.