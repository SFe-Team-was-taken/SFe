# Section 5: "info-list" chunk

## 5.1 "ifil" subchunk

### For compatibility

WORD wMajor = 2 or 3 (SFe32)

- wMajor=3 is used if the Werner SF3 sample format is used.
- Otherwise, use wMajor=2

WORD wMinor = 128 (SFe32)

- Legacy SF players might not support wMajor=4.
- SFe32 files technically appear as Version 2.128/3.128.

The size must be exactly 4 bytes. Reject files with an "ifil" subchunk that isn't 4 bytes as "Structurally Unsound".

### Using the specification version

Alternatively, the wMajor and wMinor can be set in the same way as the specification version, for example wMajor=4, wMinor=0 becomes wMajor=3, wMinor=128.

### In case of missing ifil subchunk

If the "ifil" subchunk is missing, either:

- Assume version 3.128 or 4.0.
- Reject the file as "Structurally Unsound".

* * *

## 5.1a Versioning rules

In SFe32, you can use two rules. Either:

- the value of wMajor remains 2 or 3, depending on if Werner SF3 is used
    - The value of wMinor counts up from 128.
    - It increases by one when a change is made to the format.
    - Later versions of the specification (4.01 onwards) will include a translation table to convert specification versions to SFe32 versions.
- the value of wMajor and wMinor correspond to the specification version

To signify that the SFe file has been created to a draft specification, please use the description.

* * *

## 5.2 "isng" subchunk

A new default isng sub-chunk value is used in SFe: "SFe32 version 4"

- SF version 4 players should recognise this and remove the default velocity related filter used in SoundFont(R) 2.04.
- The ten "Default Modulators" will also be disabled by default. Default modulation definition will be added in SFe version 4.01.
- In the case of a missing isng chunk, files with an ifil sub-chunk with wMajor = 2 or 3 and wMinor >= 128, assume an isng sub-chunk value of "SFe32 version 4". Don't assume "EMU8000".

Reject anything not terminated with a zero byte, and assume the value "SFe32 version 4". Do NOT assume "EMU8000" by default.

* * *

## 5.3 "INAM" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "INAM" subchunk contains an UTF-8 string of up to 256 bytes.
- Example of value: "GM Sound Set" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.4 "irom" subchunk

- Read the Soundfont(r) 2.04 specification for info on how to use ROM samples.
- The ROM emulator is optional in SFe32 programs.
- This subchunk will eventually be reused for other features in a future version of this specification.

* * *

## 5.5 "iver" subchunk

- Read the Soundfont(r) 2.04 specification for info on how to use ROM samples.
- The ROM emulator is optional in SFe32 programs.
- This subchunk will eventually be reused for other features in a future version of this specification.

* * *

## 5.6 "ICRD" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "ICRD" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "September 4, 2024" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.7 "IENG" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "IENG" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "SF Author" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.8 "IPRD" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "IPRD" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "SFe64 Players" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.9 "ICOP" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "ICOP" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "Copyright (C) All Rights Reserved." (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.10 "ICMT" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "ICMT" subchunk contains an UTF-8 string of up to 65,536 bytes.
- Example of value: "This file contains 128 instruments and a drum kit." (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.11 "ISFT" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "ISFT" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "SFe Editor version 4.00" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.12 "ISFe" subchunk

This would contain additional metadata for SFe specific features. Currently, in version 4.00, this is empty.

* * *

&nbsp;