# Aardvark 1.0 Specification

## Variables
Variables can be declared with `let` and given a value with `=`. Once a variable has been declared with `let`, it does not need to be re-declared. Types are optional, and, if present, go before the variable name.
Variable names CANNOT start with a number or an underscore (_). They may not include reserved symbols and may not be the same as a keyword. Variable names are case sensitive. Variables, when declared, are only accessible in the current scope and all sub-scopes.
Example:
```adk
let Number x # Declare
x = 5 # Initialize

let Number y = 5 # Declare and initialize

let z = 5 # Declare and initialize with automatic type inference
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

### Escape Sequences
TODO

## Control
Basic control in Aardvark include `if`, `while`, `for`, `switch`, ``

## Include
```adk
include x, y
include y, z from x
from x include y, z
include {a: b, c} from x
```

## Operators
TODO

## Functions
TODO

## Typing
TODO

## Classes / Types
TODO

## Arrays
TODO

## Objects
TODO