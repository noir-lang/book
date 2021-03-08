# Features Coming Soon

### If Statement / Ternary Expression

It is possible to emulate conditional branching with a multiplexer in Noir as of writing. However, this may not be intuitive for most. This can be sugared with an if statement or a ternary expression.

### Structures

Currently only primitives types are available. This does not hinder expressiveness, however for large circuits, readability will be harmed without structs. 

### Isize

Signed integers such as i32 and i64 allow one to express more circuits.

### Recursion

Recursion is becoming feasible in circuits, hence Noir will have native support for it. Currently, only composition is supported. 