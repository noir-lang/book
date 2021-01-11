# Control Flow

## Loops

Noir has one kind of loop, the `for-loop`. For loops allow you to repeat a block of code multiple times.

The following block of code between the braces is ran 10 times.

```rust,noplaypen
for i in 0..10 {
    // do something
}
```

For loops are expressions, so each iteration of the loop produces a value which is collected into an array.

The following code produces an array of 10 values, each element contains the same values from 0 to 9.

```rust,noplaypen
let my_arr = for i in 0..10 {
    i
};
```

## If Expressions

> Currently, these are not supported in the language.