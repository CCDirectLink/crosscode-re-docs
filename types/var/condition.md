# Var Condition



```
Expr => "(" Expr ")" | "!" Expr | Expr Op Expr | Number | String | Literal | Var

Op => "!=" | "==" | "<=" | ">=" | "<" | ">" | "=" | "+" | "-" | "%" | "*" | "AND" | "OR" | "&&" | "||"

Number => "-"? Digit+ ("." Digit+)?

Digit => "0" .. "9"

String => "\"" (EscapedChar | /[^"]/)* "\"" | "'" (EscapedChar | /[^']/)* "'"

EscapedChar => "\\" /[.]/


Literal => "true" | "false" | "null"

Var => VarChar+

VarChar => /\w/ | "." | "/" | "-" | "[" | "]"

Whitespace => "\x20"
```

.. means match between character range including the start and end characters.

Regular Expressions start and end with a /. 


This is roughly how it is processed.
And Whitespace is matched and ignored when processing the next token.
