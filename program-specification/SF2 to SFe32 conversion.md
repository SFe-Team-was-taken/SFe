# SF2 to SFe32 converter program specification

## An SF2 to SFe32 converter may be constructed in many different ways.

SFe32 files are very similar in structure to SF2 files, with these important differences:

- ifil version is updated from 2.04 to 2.128
- isng is updated to "SFe32 version 4"
- sm32 and scom sub-chunks are added
- Unused wPreset and wBank bits are used
- dwLibrary, dwGenre and dwMorphology implemented
- New SFModulator enum options
- Default modulators 1-4 are removed
- SFe32 ROM emulator and subtractive synthesis support

### Conversion from SF2 to SFe32:

- Upgrade the ifil version in the header from wMajor=2, wMinor=4 to wMajor=2, wMinor=128.
- Overwrite the isng value with "SFe32 version 3".
- Add an scom sub-chunk to already compressed files. Port sample data directly into the converted file.
- Add modulators to instruments that replace the default modulators 1-4, if used.
- Remove modulators that override the default modulators 1-4.

### Conversion from SFe32 to SF2.04:

- Downgrade the ifil version in the header from wMajor=2, wMinor=128 to wMajor=2, wMinor=4.
- Overwrite the isng value with "X-Fi".
- Decompress the samples, and remove the scom sub-chunk.
- Downsample any 32-bit samples to 24-bit, and remove the sm32 sub-chunk.
- Convert all 8-bit samples to 16-bit by moving the sample data to the smpl sub-chunk.
- If the first 8 bits of either wPreset or wBank are identical to another patch, keep only the patch with bits 9-16 clear. If this is not found, keep only the last of the patches in the record. Clear bits 9-16 of all patches afterwards.
- Remove all modulators that implement default modulators 1-4.
- Add modulators that override the default modulators 1-4.

Conversion from SFe32 to SF2.01:

- Downgrade the ifil version in the header from wMajor=2, wMinor=128 to wMajor=2, wMinor=1.
- Overwrite the isng value with "EMU8000" or "E-mu 10K1".
- Decompress the samples, and remove the scom sub-chunk.
- Downsample any 24-bit or 32-bit samples to 16-bit, and remove the sm24 and sm32 sub-chunks.
- Convert all 8-bit samples to 16-bit by moving the sample data to the smpl sub-chunk.
- If the first 8 bits of either wPreset or wBank are identical to another patch, keep only the patch with bits 9-16 clear. If this is not found, keep only the last of the patches in the record. Clear bits 9-16 of all patches afterwards.
- Remove all modulators that implement default modulators 1-4.
- Add modulators that override the default modulators 1-4.