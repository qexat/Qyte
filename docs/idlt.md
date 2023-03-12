# IDentifier Lookup Table

## Elements

The table ends when two consecutive `NUL` bytes are encountered.

### Header

Size: 8 bytes.

The first four bytes must be `IDLT` (`01001001 01000100 01001100 01010100`).

The last four bytes are the result of the following formula: `maximum identifier size - 255`.\
Setting them to 0 discards the limit ; see the [example](#example).

### Entry

-   Key: 2 bytes. Range from `00000000 00000001` to `11111110 11111111`, allowing 65279 entries (the 257 other possible keys are reserved).
-   ID: variable size. Implementation detail: a maximum size might be set up -- if so, it must be at least 256 bytes.

The byte `11111111` marks the end of the entry -- this implies that the corresponding ASCII character should NEVER be allowed in your language identifiers.

## Example

Let an IDLT with `x`, `y` and `z` as registered identifiers.

Raw:

```rs
01001001010001000100110001010100000000000000000000000000000000000000000000000001011110000000000000000000000000100111100100000000000000000000001101111010000000000000000000000000
```

Formatted:

```rs
01001001 01000100 01001100 01010100  // IDLT Header
00000000 00000000 00000000 00000000  // ID max size (none)
00000000 00000001 01111000 11111111  // Row: key=1, id=x
00000000 00000010 01111001 11111111  // Row: key=2, id=y
00000000 00000011 01111010 11111111  // Row: key=3, id=z
00000000 00000000                    // END
```
