# SFe64 error messages 4.00.20240904

|     |     |     |     |
| --- | --- | --- | --- |
| **Error name** | **Severity** | **Description** | **First version** |
| File is Structurally Unsound!  <br>Chunk size incorrect: \[name of chunk\]! | Fatal | A chunk or sub-chunk size is incorrect. | 4.00 |
| File is Structurally Unsound!  <br>Main chunk order mismatch! | Discretion | The three main subchunks are in the wrong order. | 4.00 |
| File is Structurally Unsound!  <br>File version subchunk corrupt! | Discretion | The ifil sub-chunk is not exactly four bytes long. | 4.00 |
| Warning!  <br>Null byte not found in information data: \[name of sub-chunk\] | Non-fatal | Null bytes are not found in a sub-chunk in the info chunk. | 4.00 |
| Warning!  <br>Odd sub-chunk size in information data: \[name of sub-chunk\] | Non-fatal | Size of a sub-chunk in the information data is an odd number of bytes. | 4.00 |
| Warning!  <br>Missing ROM: \[irom value\]! Not loading ROM samples! | Non-fatal | The ROM was not found. Missing ROM in soundcard (if present), or no ROM dump present on ROM emulation players. | 4.00 |
| Warning!  <br>Incorrect ROM version: \[iver value\] referenced, \[ROM version\] provided! Do you still want to load? | Non-fatal | ROM version is incorrect or incompatible, give users option to attempt to load ROM samples. | 4.00 |
| Warning!  <br>Unrecognised sound engine: \[isng value\]! | Non-fatal | Sound engine is not recognised as "SFeXX version 4" or a legacy E-mu sound engine, defaults to "SFeXX version 4".  <br>XX is 32 or 64. | 4.00 |
| Error!  <br>No samples found! | Discretion | No samples, in-file or ROM, were found. | 4.00 |
| File is Structurally Unsound!  <br>Unsupported sample compression format! | Discretion | An incompatible compression format was found. | 4.00 |
| File is Structurally Unsound!  <br>Subchunk order mismatch in pdta! | Discretion | The nine hydra sub-chunks are in the wrong order. | 4.00 |
| File is Structurally Unsound!  <br>Missing hydra sub-chunk: \[missing subchunk\] | Fatal | One or more of the nine hydra sub-chunks are missing. | 4.00 |
| Error!  <br>Header is 32-bit internally. Treating SFe64 file as SFe32. | Non-fatal | The header of an SFe64 file is 32-bit, so the file is treated as an SFe32 file. Can be caused by renaming .sfe32 extension to .sfe64. | 4.00 |
| Error!  <br>File too large! | Discretion | A file size is above the specified limit in this program specification | 4.00 |
|     |     |     |     |
|     |     |     |     |

&nbsp;