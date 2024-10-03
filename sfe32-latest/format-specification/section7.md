# Section 7: "pdta-list" chunk

## 7.1 "Hydra" structure

Like in E-mu Systems(r) Soundfont(r) 2.04, the format SFe32 version 4.00 is based on, the structure used is known as the "hydra" structure.

According to E-mu Systems(r), a hydra has nine heads. Cut one off, and another two grow.

No major changes have been made to the structure itself. All nine of these sub-chunks are required. If any are missing, the file is "Structurally Unsound".

* * *

## 7.2 "phdr" sub-chunk

The size of this chunk is a multiple of 38 bytes.

Its structure is the same as in SF2.04.

### wPreset Changes

- In SoundFont(R) 2.04, bits 2-8 were used to select up to 128 instruments. Bits 1 and 9-16 were unused.
- Now, bits 10-16 can be used to select alternate banks.
- It's designed to be used with sysex or other commands corresponding to General MIDI extension resets.
- What bits 9-16 do in version 4:
    - Bit 9 remains reserved.
    - General MIDI(tm) 1 or 2 reset clears bits 10 and 11.
    - Roland(r) GS(r) reset clears bit 10 and sets bit 11.
    - Yamaha(r) XG(r) reset sets bit 10 and clears bit 11.
    - Roland(r) CM-64(tm)/CM-32L(tm) reset sets bits 10 and 11.
    - Bit 12 is reserved for more MIDI commands in the future. For now, bit 12 should be written as clear.
    - Bits 13-16 will not be defined. The author of the SF may use these at will with their own MIDI commands.
    - MIDI sequencers will eventually be able to set or clear all bits from 10-16 using commands.
- It allows you to run multiple standards that may conflict with each other.

### wBank Changes

- Version 4.00.1 had a new field called wBank2.
- Now, wBank stores both m.s.b. and l.s.b. bank changes (CC00 and CC32), eliminating the need for wBank2.
- wBank is still a WORD. This change was possible as wBank is 16-bit, which is sufficient to store the 14-bit bank change space. We commend E-mu for being sufficiently forward thinking to not use a CHAR/BYTE for bank selection.
- In SoundFont(R) 2.04, and SFe version 4.00.1, bit 1 was only used with bank 128 (for percussion), and bits 2-8 were used to select a single bank between 0 and 127. Bits 9-16 were unused.
- wBank is little endian.
- Now, bits 1 and are is a percussion toggle. If a bank/program change combination produces a different result for midi channel 10, bit 1 controls the percussion.
- File editors should warn the user if this issue is found.
- Bits 2-8 are now used to set the 1st bank change, and bits 10-16 are now used to set the 2nd bank change.
- The default behaviour is that bits 2-8 will set "m.s.b." (CC00) and bits 10-16 will set "l.s.b." (CC32), but version 4 compatible players should allow the user to swap CC00 and CC32 settings.
- Order in the phdr chunk in terms of wBank value.
- Summary:
    - Bit 1 = percussion toggle 1
    - Bit 2-8 = bank select m.s.b.
    - Bit 9 = percussion toggle 2
    - Bit 10-16 = bank select l.s.b.

### Definitions of dwLibrary and dwGenre

Old 2.04 fields "dwLibrary" and "dwGenre" are now defined.

- "dwLibrary" is for the overall name of the set of files contained in a library of SFe, version 4 files.
    - For example: "SFe Collection!" (with appropriate zero bytes)
- "dwGenre" is for the genre of music which the files are optimised for.
    - For example: "Rock" (with appropriate zero bytes)
- "dwMorphology" has been left out of this draft specification. It will eventually be re-introduced.

### Do not access the final sfPresetHeader entry

The last sfPresetHeader entry shouldn't need to be accessed, apart from the uses described in the SF2.04 specification.

### This is a required sub-chunk

Files without a "phdr" sub-chunk are "Structurally Unsound".

* * *

## 7.3 "pbag" sub-chunk

This refers to the "Preset Bag" of the SFe file. This sub-chunk is a multiple of 4 bytes.

Its structure is the same as in SF2.04.

All values in this sub-chunk should be used as directed in the SF2.04 specification.

### This is a required sub-chunk

Files without a "pbag" sub-chunk are "Structurally Unsound".

* * *

## 7.4 "pmod" sub-chunk

The pmod sub-chunk is a multiple of 10 bytes.

The structure is very similar to SF2.04's PMod structure, with these differences:

### New options for the SFModulator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum, and all other enums, is 2 bytes in length.

### This is a required sub-chunk

Files without a "pmod" sub-chunk are "Structurally Unsound".

* * *

## 7.5 "pgen" sub-chunk

The pgen sub-chunk is a multiple of 4 bytes, like in SF2.04.

The structure and type definitions are the same as in SF2.04:

### New options for the SFGenerator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum is 2 bytes in length.

### This is a required sub-chunk

Files without a "pgen" sub-chunk are "Structurally Unsound".

* * *

## 7.6 "inst" sub-chunk

The inst sub-chunk is a multiple of 22 bytes.

### This is a required sub-chunk

Files without an "inst" sub-chunk are "Structurally Unsound".

* * *

## 7.7 "ibag" sub-chunk

This refers to the "Instrument Bag" of the SFe32 file.

This sub-chunk is a multiple of 4 bytes. This is like the pbag sub-chunk.

All values in this sub-chunk should be used as directed in the SF2.04 specification.

### This is a required sub-chunk

Files without an "ibag" sub-chunk are "Structurally Unsound".

* * *

## 7.8 "imod" sub-chunk

The imod sub-chunk is a multiple of 10 bytes, like the pmod sub-chunk.

The structure is very similar to SF2.04's imod structure, with these differences:

### New options for the SFModulator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum, and all other enums, is 2 bytes in length.

### Preset and instrument modulators

The Preset Modulator values are added to the Instrument Modulator values, and that is the final modulator used.

### This is a required sub-chunk

Files without an imod sub-chunk are "Structurally Unsound".

* * *

## 7.9 "igen" sub-chunk

The igen sub-chunk is a multiple of 4 bytes, like the pgen sub-chunk.

### New options for the SFGenerator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum is 2 bytes in length.

### This is a required sub-chunk

files without an "igen" sub-chunk are "Structurally Unsound".

* * *

## 7.10 "shdr" sub-chunk

The shdr sub-chunk contains the headers for the sample data.

It is a multiple of 46 bytes.

### Sample Rate Limit Changes

- In both SFe32, sample rates (dwSampleRate) are stored as a 32-bit integer. This is the same behaviour as seen in the legacy SoundFont(r) 2.04 format. This results in a theoretical maximum sample rate of 4,294,967,295 Hz.
- In the legacy SoundFont(r) 2.04 specification, E-mu suggested that sample rates of below 400 Hz or above 50000 Hz should be avoided as some legacy hardware platforms may not be able to reproduce these sounds. This is not a limitation of the specification, but rather a limitation of legacy sound cards.
- Despite this, Creative did not use 16-bit integers for sample rate in SF 2.04. It is thus safe to use sample rates in excess of 50000 Hz. If a sample rate of below 400 Hz or above 50000 Hz is encountered, no attempt should be made to change the sample rate.
- A zero sample rate should be reset.

### sfSampleType and Werner SF3

Bit 4 of "sfSampleType" is reserved for Werner SF3 usage.

- Read the draft Werner SF3 specification for information!
- This specification is available at: [SoundFont3Format · FluidSynth/fluidsynth Wiki (github.com)](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format)

The "sfSampleType" enum is 2 bytes in length.

### This is a required sub-chunk

Files without an "shdr" sub-chunk are "Structurally Unsound".