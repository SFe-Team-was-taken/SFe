# Section 5: "info-list" chunk

## 5.1 "ifil" subchunk

WORD wMajor = 4 (SFe64)

- The version is 4.0, so the wMajor is changed from 2 (in v2.04) to 4.

WORD wMinor = 0 (SFe64)

- The minor version has been reset to 0 because the wMajor has changed to 3.

WORD wMajor = 2 or 3 (SFe32)

- wMajor=3 is used if the Werner SF3 sample format is used.
- Otherwise, use wMajor=2

WORD wMinor = 128 (SFe32)

- Legacy SF players might not support wMajor=4.
- SFe32 files technically appear as Version 2.128/3.128.

The size must be exactly 4 bytes. Reject files with an "ifil" subchunk that isn't 4 bytes as "Structurally Unsound".

If the "ifil" subchunk is missing, either:

- Assume version 3.128 or 4.0.
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

In SFe32 version 4, the value of wMajor remains 2 or 3, depending on if Werner SF3 is used.

- The value of wMinor counts up from 128.
- It increases by one when a change is made to the format.
- Later versions of the specification (4.01 onwards) will include a translation table to convert specification versions to SFe32 versions.

To signify that the SFe file has been created to a draft specification, please use the description.

* * *

## 5.2 "isng" subchunk

A new default isng sub-chunk value is used in SFe: "SFe32 version 4" (SFe32) or "SFe64 version 4" (SFe64)

- SF version 4 players should recognise this and remove the default velocity related filter used in SoundFont(R) 2.04.
- The ten "Default Modulators" will also be disabled by default. Default modulation definition will be added in SFe version 4.01.
- In the case of a missing isng chunk, files with an ifil sub-chunk with wMajor = 2 or 3 and wMinor >= 128, assume an isng sub-chunk value of "SFe32 version 4". Don't assume "EMU8000".
- In the case of a missing isng chunk, files with an ifil sub-chunk with wMajor >= 4, assume an isng sub-chunk value of "SFe64 version 4". Don't assume "EMU8000".

Reject anything not terminated with a zero byte, and assume the value "SFe64 version 4". Do NOT assume "EMU8000" by default.

* * *

## 5.3 "INAM" subchunk

The maximum length for a SFe64 file name will be increased.

- Maximum length is increased to 65536 Characters.
- The "INAM" subchunk contains an UTF-8 string of up to 65536 bytes.
- Example of value: "GM Sound Set" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

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

The maximum length for a SFe64 file's creation date will be increased.

- Maximum length is increased to 65536 Characters.
- The "ICRD" subchunk contains a UTF-8 string of up to 65536 bytes.
- Example of value: "September 1, 2022" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.7 "IENG" subchunk

The maximum length for a SFe64 file's author name(s) will be increased.

- Maximum length is increased to 65536 Characters.
- The "IENG" subchunk contains a UTF-8 string of up to 65536 bytes.
- Example of value: "SF Author" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.8 "IPRD" subchunk

The maximum length for a SFe64 file's product name will be increased.

- Maximum length is increased to 65536 Characters.
- The "IPRD" subchunk contains a UTF-8 string of up to 65536 bytes.
- Example of value: "SFe64 Players" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.9 "ICOP" subchunk

The maximum length for a SFe64 file's copyright notice will be increased.

- Maximum length is increased to 65536 Characters.
- The "ICOP" subchunk contains a UTF-8 string of up to 65536 bytes.
- Example of value: "Copyright (C) All Rights Reserved." (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.10 "ICMT" subchunk

The maximum length for a SFe64 file's description will be increased.

- Maximum length is increased to 4 Billion Characters.
- The "ICMT" subchunk contains an UTF-8 string of up to 4,294,967,296 bytes.
- Example of value: "This file contains 128 instruments and a drum kit." (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.11 "ISFT" subchunk

The maximum length for a SFe64 file's software list will be increased.

- Maximum length is increased to 65536 Characters.
- The "ISFT" subchunk contains a UTF-8 string of up to 65536 bytes.
- Example of value: "SFe Editor version 4.00" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound".

* * *

## 5.12 "ISFe" subchunk

This would contain additional metadata for SFe specific features. Currently, in version 4.00, this is empty.

* * *

&nbsp;