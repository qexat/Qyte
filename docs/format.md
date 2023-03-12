# Qyte format

The recommended (and generated) file extension is `.qyte`.

## Header (16 bytes)

### Name

Should always be `QYTE`.

> Total size: 4 bytes

### Version

-   Major: 1 byte
-   Minor: 2 bytes
-   Patch: 2 bytes

Example: `v7.2.28`

-   `00000111`
-   `00000000 00000010`
-   `00000000 00011100`

**Compatibility rules**

-   Major not matching => `ERROR`
-   Minor not matching => `INFO`
-   Patch not matching => `IGNORED`

> Total size: 5 bytes

// TODO

## Tables

### Source file

-   path
-   hash
-   encoding
-   // TODO

### IDLT

See the dedicated [resource](./idlt.md).

## Payload

// TODO
