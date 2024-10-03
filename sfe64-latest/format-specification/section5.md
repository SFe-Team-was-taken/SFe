# Section 5: "info-list" chunk

## 5.1 "ifil" subchunk

WORD wMajor = 4

- The version is 4.00, so the wMajor is changed from 2 (in v2.04) to 4.

WORD wMinor = 0

- The minor version has been reset to 0 because the wMajor has changed to 3.

The size must be exactly 4 bytes. Reject files with an "ifil" subchunk that isn't 4 bytes as "Structurally Unsound".

If the "ifil" subchunk is missing, either:

- Assume version 4.0.
- Reject the file as "Structurally Unsound".

* * *

## 5.1a Versioning rules

In SFe64 version 4, new versioning rules are used to replace the old ones.

The value of wMajor increases every time a change is made to the format that makes it incompatible with existing players.

- There will be at least 6 months between the initial draft specification of a new version and the release of the final specification.
- Older wMajor versions must be supported, either directly or via translation to the latest version.
- We strive to minimise the number of these updates whenever possible in favour of updates that are backward compatible.

The value of wMinor increases every time a change is made to the format while retaining backwards compatibility.

- These updates generally have only one or two draft specification before the final specification releases.
- Feature updates in these versions are smaller.

To signify that the SFe file has been created to a draft specification, please use the description.

* * *

## 5.2 "isng" subchunk

A new default isng sub-chunk value is used in SFe: "SFe32 version 4" (SFe32) or "SFe64 version 4" (SFe64)

- SF version 4 players should recognise this and remove the default velocity related filter used in SoundFont(R) 2.04.
- The ten "Default Modulators" will also be disabled by default. Default modulation definition will be added in SFe version 4.01.
- In the case of a missing isng chunk, files with an ifil sub-chunk with wMajor = 2 or 3 and wMinor >= 128, assume an isng sub-chunk value of "SFe32 version 4". Don't assume "EMU8000". This is for backwards compatibility with SFe32.
- In the case of a missing isng chunk, files with an ifil sub-chunk with wMajor >= 4, assume an isng sub-chunk value of "SFe64 version 4". Don't assume "EMU8000".

Reject anything not terminated with a zero byte, and assume the value "SFe64 version 4". Do NOT assume "EMU8000" by default.

* * *

## 5.3 "INAM" subchunk

This is mostly the same as in Soundfont(r) 2.04, but UTF-8 is now used instead of ASCII.

- The "INAM" subchunk contains an UTF-8 string of up to 256 bytes.
- Example of value: "GM Sound Set" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.4 "irom" subchunk

- Read the Soundfont(r) 2.04 specification for info on how to use ROM samples.
- The ROM emulator should be implemented in SFe64 programs.
- This subchunk will eventually be reused for other features in a future version of this specification.

* * *

## 5.5 "iver" subchunk

- Read the Soundfont(r) 2.04 specification for info on how to use ROM samples.
- The ROM emulator should be implemented in SFe64 programs.
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