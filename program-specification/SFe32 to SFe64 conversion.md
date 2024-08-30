# SFe32 to SFe64 converter program specification

### Conversion of SFe32 to SFe64 should be possible without loss.

Differences between SFe32 and SFe64:

- ifil is updated from 2.128 or 3.128 to 4.00
    
- isng is updated from "SFe32 version 4" to "SFe64 version 4"
    
- Info chunk field size increases from 8/16-bit to 16/32-bit.
    
- Expanded achNames from 20 chars to 256 chars.
    
- Category field in phdr sub-chunk.
    
- Sample description in shdr sub-chunk.
    
- Seven secondary loops in shdr sub-chunk.
    
- pbag/ibag sub-chunk size extended.
    
- 32-bit signed modulators.
    
- New dsp effects.
    
- Reverb and chorus types.
    

### Conversion of SFe32 to SFe64:

- Convert the RIFF format to RIFF64.
- Upgrade the ifil version in the header from wMajor=2, wMinor=128 to wMajor=4, wMinor=0.
- Overwrite the isng value with "SFe64 version 4".
- Expand the fields in the pdta chunk to the SFe64 specification.
- Add dwCategory, achSampleDescription\[256\] fields.
- Add seven secondary loops in the shdr sub-chunk.

### Conversion of SFe64 to SFe32:

- Convert the RIFF64 format to RIFF.
- Downgrade the ifil version in the header from wMajor=3, wMinor=0 to wMajor=2, wMinor=128.
- Overwrite the isng value with "SFe32 version 4".
- Truncate 32-bit info chunk fields to 65536 characters, and 16-bit info chunk fields to 256 characters.
- Truncate achNames to 20 characters.
- Remove dwCategory, achSampleDescription\[256\] fields.
- Remove any secondary loops in the shdr sub-chunk.
- Remove all modulators that refer to effects beyond #60.
- Filesize above 4GB can't be converted to SFe32. They can be split.