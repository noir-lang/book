# Mutability

All variables in Noir are immutable and cannot be made mutable. Due to this, Noir will at some stages borrow functional programming concepts.

### Why immutability?

Witnesses in a proving system are immutable in nature. Noir aims to _closely_ mirror this setting without applying additional overhead to the user. If a developer encounters a variable _a_ he can lookup its definition to deduce its value.

> The last section may be somewhat invalidated, if temporary scopes and shadowing is introduced.