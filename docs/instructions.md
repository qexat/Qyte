# Instructions

Form: `[OP CODE] [FUNC CODE] [DEST ID KEY] [ARGS CODE] [ARGS KEYS]`

| OP Kind    | OP CODE |
| ---------- | ------- |
| Arithmetic | `0b00`  |
| Logical    | `0b01`  |
| Load/Store | `0b10`  |
| Branching  | `0b11`  |

> The pseudo-instructions fall into one of the four categories that suit the most -- they do not have their own.

| Operands Kind  | ARGS CODE |
| -------------- | --------- |
| `ids1`, `ids2` | `0b00`    |
| `ids1`, `ims2` | `0b01`    |
| `ims1`, `ids2` | `0b10`    |
| `ims1`, `ims2` | `0b11`    |

In short, bit is set to `0` if the value is from an identifier, and to `1` if it's from an immediate.

> Note: The target kind does not affect the code above.

## Arithmetic

### Function code

-   First digit: binary (0) or unary (1)
-   Second digit: positive polarity (0) or negative polarity (1)
-   Third & fourth digit: magnitude

### Magnitude

| Magnitude | value |
| --------- | ----- |
| 1         | 0b00  |
| 2 (full)  | 0b01  |
| 2 (half)  | 0b10  |
| 3         | 0b11  |

> The integer division is of magnitude 2 (full) because for an intdiv of `x // y == z`, the necessary operation to get `x` back from `y` and `z` is the multiplication, which is also of magnitude 2.\
> On the other hand, the modulo is of magnitude (half) because the reverse operation is the addition, which is of magnitude 1.\
> i.e.: `x == y * z + r`

### Operations

| Operation | FUNC CODE | Comment                      |
| --------- | --------- | ---------------------------- |
| `ADD`     | `0b0000`  | `n + p`                      |
| `MUL`     | `0b0001`  | `n * p`                      |
| `POW`     | `0b0011`  | `n ** p`                     |
| `SUB`     | `0b0100`  | `n - p`                      |
| `INTDIV`  | `0b0101`  | `n // p`                     |
| `MOD`     | `Ob0110`  | `n % p`                      |
| `ROOT`    | `0b0111`  | `n ** (1 / p)`               |
| `ABS`     | `0b1000`  | `\|n\|`                      |
| `POW2`    | `0b1011`  | Equivalent to `n ** 2`       |
| `NEG`     | `0b1100`  | Equivalent to `0 - n`        |
| `SQROOT`  | `0b1111`  | Equivalent to `n ** (1 / 2)` |

## Logic

### Function code

-   First digit: binary (0) or unary (1)
-   Second digit: setop (0) or shift (1)
-   Third & fourth digit: ID

### Operations

| Operation | FUNC CODE | Comment   |
| --------- | --------- | --------- |
| `AND`     | `0b0000`  | `n & p`   |
| `OR`      | `0b0001`  | `n \| p`  |
| `XOR`     | `0b0010`  | `n ^ p`   |
| `SLL`     | `0b0100`  | `n << p`  |
| `SRL`     | `0b0101`  | `n >>> p` |
| `SRA`     | `0b0110`  | `n >> p`  |
| `NEG`     | `0b1000`  | `~n`      |

## Load/Store

### Function code

// TODO

## Branching

### Function code

// TODO
