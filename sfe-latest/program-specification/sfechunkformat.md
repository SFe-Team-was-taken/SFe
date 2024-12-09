# SFe chunk header converter program specification 4.0.11

Conversion between chunk header types should be possible without loss.

### Conversion of 32-bit static to 64-bit static:

- Replace `RIFF` with `RF64`.
- Add a `ds64` chunk with chunk size.
- Set `ckSize` to `FF FF FF FF`.
- Replace `sfbk` with `sfen`.

### Conversion of 64-bit static to 32-bit static:

- Make sure file size does not exceed 4GiB.
- Set `ckSize` to the value of `ds64`.
- Delete `ds64`.
- Replace `RF64` with `RIFF`.
- Rename `sfen` to `sfbk` (SFe 4).

### Conversion between 32-bit static and RIFX:

- Replace `RIFF` with `RIFX` (or vice versa).
- Swap the bytes to convert between big endian and little endian.
