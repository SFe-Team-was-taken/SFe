|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Error id** | **Error name** | **Severity** | **Description** | **First version** | **SFe32 or SFe64** |
| 0   | File is Structurally Unsound!  <br>Chunk size incorrect: \[name of chunk\]! | Fatal | A chunk or sub-chunk size is incorrect. | 4.00 | All |
| 1   | File is Structurally Unsound!  <br>Main chunk order mismatch! | Discretion | The three main subchunks are in the wrong order. | 4.00 | All |
| 2   | File is Structurally Unsound!  <br>File version subchunk corrupt! | Discretion | The ifil sub-chunk is not exactly four bytes long. | 4.00 | All |
| 3   | Warning!  <br>Null byte not found in information data: \[name of sub-chunk\] | Non-fatal | Null bytes are not found in a sub-chunk in the info chunk. | 4.00 | All |
| 4   | Warning!  <br>Odd sub-chunk size in information data: \[name of sub-chunk\] | Non-fatal | Size of a sub-chunk in the information data is an odd number of bytes. | 4.00 | All |
| 5   | Warning!  <br>Missing ROM: \[irom value\]! Not loading ROM samples! | Non-fatal | The ROM was not found. Missing ROM in soundcard (if present), or no ROM dump present on ROM emulation players. | 4.00 | All |
| 6   | Warning!  <br>Incorrect ROM version: \[iver value\] referenced, \[ROM version\] provided! Do you still want to load? | Non-fatal | ROM version is incorrect or incompatible, give users option to attempt to load ROM samples. | 4.00 | All |
| 7   | Warning!  <br>Unrecognised sound engine: \[isng value\]! | Non-fatal | Sound engine is not recognised as "SFeXX version 4" or a legacy E-mu sound engine, defaults to "SFeXX version 4".  <br>XX is 32 or 64. | 4.00 | All |
| 8   | Error!  <br>No samples found! | Discretion | No samples, in-file or ROM, were found. | 4.00 | All |
| 9   | File is Structurally Unsound!  <br>Unsupported file-wide compression format! | Fatal | Incompatible and proprietary compression format was used, like .SFARK, .SFPACK or .SF2PACK. The commercial license for these formats can no longer be purchased; these formats should not be used. | 4.00 | All |
| 10  | File is Structurally Unsound!  <br>Unsupported sample compression format! | Discretion | An incompatible compression format was found. | 4.00 | All |
| 11  | File is Structurally Unsound!  <br>Subchunk order mismatch in pdta! | Discretion | The nine hydra sub-chunks are in the wrong order. | 4.00 | All |
| 12  | File is Structurally Unsound!  <br>Missing hydra sub-chunk: \[missing subchunk\] | Fatal | One or more of the nine hydra sub-chunks are missing. | 4.00 | All |
| 13  |     |     |     |     |     |
| 14  |     |     |     |     |     |
| 15  |     |     |     |     |     |
| 16  |     |     |     |     |     |
| 17  |     |     |     |     |     |

Error ID's are used here to enumerate the errors. These are not the actual codes to return in SF3 implementations.