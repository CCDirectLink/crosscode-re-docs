# VarName

Rules:
Anything in between [] must either be a digit or variable
If it is between []:
- a number? The number is returned
- anything else? It is treated as a variable name. The value of the variable is returned.
The result is going to have a dot prepending to it if should be treated as an accessor.
- Anything being access must either have a valid value or is also an object

Examples:

```js
// variables:
a = 1
b = [32,48]

// expressions:
b[a] // turns into b.1
b[b[a]] // turns into b[b.1] which turns into b.48
b[32][48] // turns into b.32.48
b[b.0][b.1] // also turns into b.32.48 
b[b.0.1] // is equivalent to b[b[0].1] which implies b[0] is an object
         // turns into b[32.1] since 32 is not an object, it turns into 
         // b.null 

// All ] must proceed with . ] or [ otherwise the output will return null 
] // special case: If there is no [ in the input then it will return the input

// ] must be after [
][ // returns null

// All [ must have a ] or it will return null
[]] // returns null

[ // throws an error
```