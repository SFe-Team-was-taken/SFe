# SFe program specification

This specification is written as a baseline that you can expect any program that implements the SFe standard to meet.

All SFe programs must meet these minimum requirements. If they do not, guarantees that an SFe file will work on the program can not be made.

If an implementation is unable to reach the layering requirements without crashing, it is not entirely SFe compatible.

### 1\. File format specifications

|     |     |     |     |
| --- | --- | --- | --- |
|     |     | **SFe32** | **SFe64** |
| **1A** | **File size representation** | Unsigned 32-bit integer  <br>You must not use signed integers | Unsigned 64-bit integer  <br>You must not use signed integers |
| **1Bi** | **File size limit** | 4 GiB (4.29 GB) or greater  <br>Or system memory | 16 EiB (18.4 EB) or greater  <br>Or system memory |
| **1Bii** | **TSC mode** | Optional | Optional |
| **1C** | **Sample streaming** | System memory and disk streaming | System memory and disk streaming |
| **1D** | **Total file size limit** | 32 GiB (34.4 GB) or greater | 4 ZiB (4.72 ZB) or greater |
| **1Ei** | **Multiple files** | 8 or more  <br>You may use any file listing system  <br>(Example: SFLIST files) | 256 or more  <br>You may use any file listing system  <br>(Example: SFLIST files) |
| **1Eii** | **SF call function** | Supported | Supported |
| **1F** | **Legacy support** | SF2.01, Werner SF3  <br>SynthFont Custom Features optional | SF2.01, SF2.04, and Werner SF3  <br>SynthFont Custom Features optional |
| **1G** | **Header support** | "RIFF" | "RIFF", "RF64", "BW64" |
| **1H** | **Sample compression** | Werner SF3 format  <br>Uncompressed, FLAC, Opus, Vorbis  <br>Proprietary formats forbidden | Werner SF3 format  <br>Uncompressed, FLAC, Opus, Vorbis  <br>Proprietary formats forbidden |
| **1I** | **File extension** | \-  <br>SFe32: .sfe32, .sfe  <br>SF2.04: .sf2  <br>Any other format is allowed | SFe64: .sfe64, .sfe  <br>SFe32: .sfe32, .sfe  <br>SF2.04: .sf2  <br>Any other format is allowed |
| **1J** | **Information/Metadata** | Chunks and size limits defined by 2.04 | New chunks and size limits |

### 2\. Sample specifications

|     |     |     |     |
| --- | --- | --- | --- |
|     |     | **SFe32** | **SFe64** |
| **2A** | **Maximum sample rate** | 50 000 Hz or greater | 96 000 Hz or greater |
| **2B** | **Sample bit depth** | 16 bit or greater  <br>Ignore unsupported sdta sub-chunks | 24 bit or greater  <br>Ignore unsupported sdta sub-chunks |
| **2C** | **Individual sample length** | 16 777 216 samples or greater | 281 474 976 710 656 samples or greater |
| **2D** | **Loop point sets** | 1   | 1   |
| **2E** | **Sample linking** | Mono, Left/Right, "Link"  <br>Includes ROM samples | Mono, Left/Right, "Link"  <br>Includes ROM samples |
| **2F** | **Number of channels** | Mono, Stereo | Mono, Stereo, Surround (unlimited) |
| **2G** | **Sample name length** | 20 characters | Display 64-256 characters  <br>Write 256 characters |

### 3\. Instrument specifications

|     |     |     |     |
| --- | --- | --- | --- |
|     |     | **SFe32** | **SFe64** |
| **3A** | **Samples per instrument** | 4096 or greater | 16384 or greater |
| **3B** | **Simultaneous sample playback** | 32 or greater | 64 or greater |
| **3C** | **Built in modulators** | Old modulator set, fixed | None |
| **3D** | **LFO** | Single type | Multi type |
| **3E** | **Enumerators** | SFe32 set | SFe32 set plus extra modulators |
| **3F** | **Sound effects** | Single type chorus and reverb | Multiple type chorus and reverb |
| **3G** | **Instrument name length** | 20 characters | Display 64-256 characters  <br>Write 256 characters |

### 4\. Preset specifications

|     |     |     |     |
| --- | --- | --- | --- |
|     |     | **SFe32** | **SFe64** |
| **4A** | **Instruments per preset** | 16 or greater | 64 or greater |
| **4B** | **Simultaneous sample playback** | 256 or greater  <br>Or up to polyphony limit | 512 or greater  <br>Or up to polyphony limit |
| **4C** | **Sound effects** | Single type chorus and reverb | Multiple type chorus and reverb |
| **4D** | **Instrument name length** | 20 characters | Display 64-256 characters  <br>Write 256 characters |

### 5\. Player specifications

|     |     |     |     |
| --- | --- | --- | --- |
|     |     | **SFe32** | **SFe64** |
| **5A** | **Polyphony limit** | 256 or greater with mono samples  <br>128 or greater with stereo samples  <br>\-  <br>\- | 512 or greater with mono samples  <br>256 or greater with stereo samples  <br>85 or greater with 5.1 samples  <br>64 or greater with 7.1 samples |
| **5B** | **Percussion toggle** | wBank bit 1 and 9 | wBank bit 1 and 9 |
| **5Ci** | **Control change 0/32 (Bank select)** | CC 0: wBank bits 2-8  <br>CC 32: wBank bits 10-16 | CC 0: wBank bits 2-8  <br>CC 32: wBank bits 10-16 |
| **5Cii** | **Control change 7/39/8**  <br>**Control change 40/10/42** | Mandatory | Mandatory |
| **5Ciii** | **Control change 1/33/2/34/4/36**  <br>**Control change 5/37/11/43/84** | CC 1 / 33 (modulation wheel) | All CC values supported |
| **5Civ** | **Control change 6/38** | GM1 data entries supported | GM1 and GM2 data entries supported |
| **5Cv** | **Control change 12/13/44/45**  <br>**Control change 16/17/18/19**  <br>**Control change 48/49/50/51**  <br>**Control change 80/81/82/83** | Mandatory | Mandatory |
| **5Cvi** | **Control change 64/66/67** | Mandatory | Mandatory |
| **5Cvii** | **Control change 68/69** | Optional | Mandatory |
| **5Cviii** | **Control change 70/71/72/73/74**  <br>**Control change 75/76/77/78/79** | CC70 variation  <br>CC71 timbre  <br>CC72 release time  <br>CC73 attack time  <br>CC74 brightness  <br>CC75 decay time  <br>CC76 vibrato rate  <br>CC77 vibrato depth  <br>CC78 vibrato delay | CC70 variation  <br>CC71 timbre  <br>CC72 release time  <br>CC73 attack time  <br>CC74 brightness  <br>CC75 decay time  <br>CC76 vibrato rate  <br>CC77 vibrato depth  <br>CC78 vibrato delay |
| **5Cix** | **Control change 91/93** | Reverb and chorus, single type | Reverb and chorus, multiple types |
| **5Cx** | **Control change 92/94/95** | GM1 level effects unit  <br>\- | GM2 level effects unit  <br>XG(r)/GS(r) unit optional |
| **5Cxi** | **Control change 96/97/98**  <br>**Control change 99/100/101** | Mandatory | Mandatory |
| **5Cxii** | **Control change 120/121/122/123**  <br>**Control change 124/125/126/127** | Mandatory | Mandatory |
| **5Di** | **GM1 reset** | Mandatory | Mandatory |
| **5Dii** | **GM2 reset**  <br>**Roland(r) GS(r) reset**  <br>**Roland(r) MT(tm)/CM(tm) reset**  <br>**Yamaha(r) XG(r) reset** | Optional | GM2 mandatory  <br>All others optional |
| **5E** | **Number of simultaneous drum kits** | 2 or more  <br>Use GM2 command | 2 or more  <br>Use GM2 command |
| **5F** | **SMF formats** | 0 and 1 | 0 and 1 |
| **5G** | **Number of channels** | 16 or greater | 64 or greater |
| **5H** | **ROM emulator** | ROM sample support or emulator | ROM emulator |