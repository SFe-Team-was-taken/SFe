# SFe32 Compatibility Specification 4.00.6

This is a non-exhaustive list of compatibility workarounds relating to the ancient Soundfont(r) 2.04 format and the new SFe version 4.

### About compatibility specification versioning

If the version number of this specification is not yet updated, then the information here is up to date for the new specification.

### SF 2.04 specification compatibility

If a legacy SF player is not fully compatible with the SF 2.0x specification, then SFe32 files might not work properly.

### INFO chunk and legacy compatibility

SFe32 files should be as compliant with the legacy standard as possible. The legacy SF2.0x standard tells implementations to ignore additional sub-chunks in the INFO chunk, therefore it is possible to use the INFO chunk for additional data related to SFe.

If SFe32 files cannot be loaded on Sound Blaster cards, then something has went wrong.

### wMajor = 4 compatibility

Legacy SF programs may not support wMajor=4. You may need to use this defined workaround:

- If the file uses the Werner SF3 sample format, use wMajor=3, wMinor=128.
- Otherwise, use wMajor=2, wMinor=128.

SFe32 files technically appear as Version 2.128 or Version 3.128 to legacy SF programs depending on if Werner SF3 sample formatting is used.

Legacy SF programs may not support wMajor=3, even if samples are uncompressed. It is safe to omit Werner SF3 structures for uncompressed SFe32 files.

### When to assume the isng sub-chunk as EMU8000

To maximise backwards compatibility with Soundfont(r) 2.x files, files with an ifil sub-chunk representing "2.04" or below should continue to assume an isng sub-chunk value of "EMU8000".

Do NOT assume "EMU8000" when the ifil sub-chunk is >=2.128.

### UTF-8 strings may be interpreted as ASCII

The SF 2.04 specification officially defines all strings as ASCII strings. Because UTF-8 is mostly backwards compatible with ASCII, the strings found in SFe files are mostly compatible with legacy SF players. Mojibake may result on legacy systems when using characters unsupported by ASCII.

Some characters use multiple bytes in UTF-8. You may not be able to use as many multi-byte characters compared to single-byte characters.

### The ISFe chunk is not 100% legacy SF2.04 conformant

Officially, according to the SF 2.04 specification, additional subchunks mean that an SFe file is not 100% conformant to the legacy SF standard.

However, said specification instructs implementations to ignore this sub-chunk if it is not recognised.

### Why are there no maximum length increases?

SFe32 does not support increased maximum length changes due to backward compatibility concerns.

To retain compatibility with legacy software:

- achPresetName's length remains 20
- wPresetBagNdx is retained instead of dwPresetBagNdx
- wGenNdx and wModNdx is retained instead of dwGenNdx and dwModNdx
- achInstName's length remains 20
- wInstBagNdx is retained instead of dwInstBagNdx
- wInstGenNdx and wInstModNdx is retained instead of dwInstGenNdx and dwInstModNdx
- achSampleName's length remains 20
- Fields in shdr chunk remain DWORDs

### How is information formatted?

One character no longer corresponds to one byte in UTF-8.

If UTF-8 cannot be used by the player, it should be displayed as Ascii.

### Sample specifications

Players fully compliant with the legacy SoundFont(R) 2.04 specification should be able to play files with 32-bit samples at 24-bit quality. However, these files may fail on players that look specifically for sm24 and reject anything else.

It is therefore not recommended to use 32-bit samples with legacy SF2.0x players. The sm32 sub-chunk is implemented in the same way as sm24 was by E-mu, to maximise compatibility.

Due to the massive size, unpracticality and compatibility implications of 32-bit samples, we recommend that you use the sm32 sub-chunk only with SFe64 files.

The legacy specification ignores an sm24 sub-chunk that is not paired with an smpl sub-chunk. Software that is compatible with SF version 2.04, but is incompatible with SFe, will not play 8-bit samples.

Legacy sound cards will also ignore lone sm24 chunks.

Actual non-standard sample bit depths (6-bit, 12-bit, 18-bit, etc.) are not supported by SFe version 4.

The recommended limits of the sample rate were 400-50000 in SoundFont(R) 2.04 due to quirks with legacy sound cards. ROM samples may still be used; therefore bit 16 should not be ignored.

### phdr sub-chunk

This sub-chunk must contain at least two entries. Failure to do so will affect the compatibility with legacy SF players.

wBank changes are not recognised by legacy SF players. On such legacy players, only the m.s.b. is retained.

Presets with l.s.b.=0 should be the first presets internally. You may also want to use VArranger's workaround: for example, "115@concertgrand".

### Generators and modulators

In case of compatibility issues, the "shAmount" and "wAmount" options have been kept in for now. They may be removed in future versions of the SFe version 4 specification.

If the SF version is below 2.128, and the isng value is equal to "EMU8000" or another E-mu sound engine:

- A 12dB low pass filter is used to ensure compatibility with the original AWE32 sound processor.
- Controller sources remain amplitude based.
- Ignore the whole modulator structure if a reserved source type is found.
- The Controller Source Type #16-#20 acts identically to the Controller Source Type #0-#4.

If the SF version is 2.04 or below, ignore the whole modulator structure if a reserved source type is found.

While default modulators 1-4 are not used in SFe version 4, SFe programs must still use them for older versions:

- If the SF version is 2.04, use the SF2.04 version of the Default Modulator 2.
- If the SF version is 2.01, use the SF2.01 version of the Default Modulator 2.
- If the sound engine is "EMU8000", trigger legacy sound card mode.
- If the sound engine is "E-mu 10K1", "E-mu 10K2", "X-Fi", "SFe32 version 4" or "SFe64 version 4", do not trigger legacy sound card mode.

Parameter units remain the same as SF2.04.

### Error handling

Legacy SF players may halt on undefined chunks. Section 10.2 of the original SF 2.01 and 2.04 specifications forbid the addition of sub-chunks to the sdta-list chunk, but Creative/E-mu themselves decided to do it anyway when developing SF 2.04 (the sm24 sub-chunk).

Legacy SF players may halt on unknown enums, which goes against the SF 2.04 specification.

### Incompatible compression formats

If an incompatible compression format is found, then the program may offer decompression of the incompatible file before use if you have permission from the original author of the compression formats.

SF compression programs are notorious for restrictive licensing; the commercial license for these formats can no longer be purchased. These formats should not be used.