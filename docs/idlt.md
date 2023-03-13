# IDentifier Lookup Table

## Elements

The table ends when a `NUL` key is encountered.

### Header

Size: 8 bytes.

The first four bytes must be `IDLT` (`01001001 01000100 01001100 01010100`).

The next byte is cut in parts:

-   The first four bits are `key size - 1` in bytes.
-   The last four bits are `ID character size - 1` in bytes ; setting it to `>0` allows for larger sets than ASCII.

The last three bytes are the result of the following formula: `maximum identifier size - 255`.\
Setting them to 0 discards the limit ; see the [example](#example).

### Entry

-   Key: its size is set above. In any case, the `NUL` key (`0`) is always reserved and cannot be used.
-   ID: variable size. Implementation detail: a maximum size might be set up -- if so, it must be at least 256 bytes.

The end of the entry is marked by `NUL` bytes ; their number depends on the ID character size that has been set above.

## Example

Let an IDLT with `x`, `hello` and `pow2` as registered identifiers.

Raw:

```rs
01001001 01000100 01001100 01010100
00000000 00000000 00000000 00000000
00000001 01111000 00000000 00000010
01101000 01100101 01101100 01101100
01101111 00000000 00000011 01110000
01101111 01110111 00110010 00000000
00000000
```

Commented:

```rs
// Header
01001001 01000100 01001100 01010100
00000000 00000000 00000000 00000000
// Contents
00000001 01111000 00000000 00000010
01101000 01100101 01101100 01101100
01101111 00000000 00000011 01110000
01101111 01110111 00110010 00000000
// END
00000000
```

Decomposed:

```rs
// Header
01001001 01000100 01001100 01010100  // IDLT
0000                                 // Key size (1 byte)
0000                                 // ID char size (1 byte)
00000000 00000000 00000000           // ID max size (none)
// Contents
00000001 01111000 00000000                                      // Entry: key=1, id='x'
00000010 01101000 01100101 01101100 01101100 01101111 00000000  // Entry: key=2, id='hello'
00000011 01110000 01101111 01110111 00110010 00000000           // Entry: key=3, id='pow2'
// End of Table (EOT)
00000000
```
