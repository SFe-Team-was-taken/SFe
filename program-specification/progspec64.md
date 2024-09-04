# SFe64 program specification

This specification is written as a baseline that you can expect any program that implements the SFe64 standard to meet.

All SFe64 programs must meet these minimum requirements. If they do not, guarantees that an SFe64 file will work on the program can not be made.

If an implementation is unable to reach the layering requirements without crashing, it is not entirely SFe64 compatible.

### 1\. File format specifications

|     |     |     |
| --- | --- | --- |
| **1A** | **File size representation** | Unsigned 64-bit integer  <br>You must not use signed integers |
| **1Bi** | **File size limit** | 16 EiB (18.4 EB) or greater  <br>Or system memory |
| **1Bii** | **TSC mode** | Optional |
| **1C** | **Sample streaming** | System memory and disk streaming |
| **1D** | **Total file size limit** | 4 ZiB (4.72 ZB) or greater |
| **1Ei** | **Multiple files** | 256 or more  <br>You may use any file listing system  <br>(Example: SFLIST files) |
| **1Eii** | **SF call function** | Supported |
| **1F** | **Legacy support** | SF2.01, SF2.04, and Werner SF3  <br>SynthFont Custom Features optional |
| **1G** | **Header support** | "RIFF", "RF64", "BW64" |
| **1H** | **Sample compression** | Werner SF3 format  <br>Uncompressed, FLAC, Opus, Vorbis  <br>Proprietary formats forbidden |
| **1I** | **File extension** | SFe64: .sfe64, .sfe  <br>SFe32: .sfe32, .sfe  <br>SF2.04: .sf2  <br>Any other format is allowed |
| **1J** | **Information/Metadata** | New chunks and size limits |

### 2\. Sample specifications

|     |     |     |
| --- | --- | --- |
| **2A** | **Maximum sample rate** | 96 000 Hz or greater |
| **2B** | **Sample bit depth** | 24 bit or greater  <br>Ignore unsupported sdta sub-chunks |
| **2C** | **Individual sample length** | 281 474 976 710 656 samples or greater |
| **2D** | **Loop point sets** | 1   |
| **2E** | **Sample linking** | Mono, Left/Right, "Link"  <br>Includes ROM samples |
| **2F** | **Number of channels** | Mono, Stereo, Surround (unlimited) |
| **2G** | **Sample name length** | Display 64-256 characters  <br>Write 256 characters |

### 3\. Instrument specifications

|     |     |     |
| --- | --- | --- |
| **3A** | **Samples per instrument** | 16384 or greater |
| **3B** | **Simultaneous sample playback** | 64 or greater |
| **3C** | **Built in modulators** | None |
| **3D** | **LFO** | Single type |
| **3E** | **Enumerators** | SFe set |
| **3F** | **Sound effects** | Single type chorus and reverb |
| **3G** | **Instrument name length** | Display 64-256 characters  <br>Write 256 characters |

### 4\. Preset specifications

|     |     |     |
| --- | --- | --- |
| **4A** | **Instruments per preset** | 64 or greater |
| **4B** | **Simultaneous sample playback** | 512 or greater  <br>Or up to polyphony limit |
| **4C** | **Sound effects** | Single type chorus and reverb |
| **4D** | **Instrument name length** | Display 64-256 characters  <br>Write 256 characters |

### 5\. Player specifications

|     |     |     |
| --- | --- | --- |
| **5A** | **Polyphony limit** | 512 or greater with mono samples  <br>256 or greater with stereo samples |
| **5B** | **Percussion toggle** | wBank bit 1 and 9 |
| **5Ci** | **Control change 0/32 (Bank select)** | CC 0: wBank bits 2-8  <br>CC 32: wBank bits 10-16 |
| **5Cii** | **Control change 7/39/8**  <br>**Control change 40/10/42** | Mandatory |
| **5Ciii** | **Control change 1/33/2/34/4/36**  <br>**Control change 5/37/11/43/84** | All CC values supported |
| **5Civ** | **Control change 6/38** | GM1 and GM2 data entries supported |
| **5Cv** | **Control change 12/13/44/45**  <br>**Control change 16/17/18/19**  <br>**Control change 48/49/50/51**  <br>**Control change 80/81/82/83** | Mandatory |
| **5Cvi** | **Control change 64/66/67** | Mandatory |
| **5Cvii** | **Control change 68/69** | Mandatory |
| **5Cviii** | **Control change 70/71/72/73/74**  <br>**Control change 75/76/77/78/79** | CC70 variation  <br>CC71 timbre  <br>CC72 release time  <br>CC73 attack time  <br>CC74 brightness  <br>CC75 decay time  <br>CC76 vibrato rate  <br>CC77 vibrato depth  <br>CC78 vibrato delay |
| **5Cix** | **Control change 91/93** | Reverb and chorus, multiple types |
| **5Cx** | **Control change 92/94/95** | GM2 level effects unit  <br>XG(r)/GS(r) unit optional |
| **5Cxi** | **Control change 96/97/98**  <br>**Control change 99/100/101** | Mandatory |
| **5Cxii** | **Control change 120/121/122/123**  <br>**Control change 124/125/126/127** | Mandatory |
| **5Di** | **GM1 reset** | Mandatory |
| **5Dii** | **GM2 reset**  <br>**Roland(r) GS(r) reset**  <br>**Roland(r) MT(tm)/CM(tm) reset**  <br>**Yamaha(r) XG(r) reset** | GM2 mandatory  <br>All others optional |
| **5E** | **Number of simultaneous drum kits** | 2 or more  <br>Use GM2 command |
| **5F** | **SMF formats** | 0 and 1 |
| **5G** | **Number of channels** | 64 or greater |
| **5H** | **ROM emulator** | ROM emulator |