# Section 7: "pdta-list" chunk

## 7.1 "Hydra" structure

Like in E-mu Systems(r) Soundfont(r) 2.04, the format SFe version 4 is based on, the structure used is known as the "hydra" structure.

According to E-mu Systems(r), a hydra has nine heads. Cut one off, and another two grow.

No major changes have been made to the structure itself. However, some of the variables inside each of the nine sub-chunks of the "hydra" structure have been changed to increase the length limits of variables. (SFe64)

- Some WORDs have been changed to DWORDs (the w at the beginning has changed to dw).
- Programs which create SFe64 files can not share exactly the same code as programs which create SFe32 files.
- Replacing the "BW64" header and "ds64" chunks with a "RIFF" header will likely not convert an SFe64 file to a file which can be played by legacy SF players. A proper conversion is required.
- Programs can be made to automatically convert the data types, headers and chunks to what is used in SFe32, with a version of 2.128 or 3.128, allowing use with legacy SF players.
- In the future, SFe64 files will have extra sub-chunks. The goal is to remove as many hardcoded size limits as possible. It will also allow us to add more fields easily, like a sample description field that is planned for the future.

All nine of these sub-chunks are required. If any are missing, the file is "Structurally Unsound".

- SFe32 will retain these nine sub-chunks in the order prescribed by SF2.04.
- If the order is incorrect, or there are extra sub-chunks in an SFe32 file, the file is "Structurally Unsound" and should be rejected.
- However, the SFe64 hydra will probably grow some more heads in the future.
- Therefore, do not assume that a file is "Structurally Unsound" if you find extra sub-chunks in SFe64.
- We will work on reworking the pdta chunk to remove as many hardcoded limits as possible (for SFe64 only).
- For now, however, the existing limits are extended slightly.
- Note that the result might not even be remotely similar to the original hydra structure.
- Existing structures will be retained to allow easy transition to newer versions of SFe64, and to provide legacy support for older versions, as well as SFe32.

Note: All structures for these sub-chunks demonstrated here are for SFe64, unless shown otherwise. Refer to the RIFF structure for SFe32.

* * *

## 7.2 "phdr" sub-chunk

The size of this chunk is a multiple of 38 bytes (SFe32).

The size of this chunk is a multiple of 280 bytes (SFe64).

Its structure is like this (SFe64):

```
struct sfPresetHeader
        {
            CHAR achPresetName[256];
            WORD wPreset;
            WORD wBank;
            DWORD dwPresetBagNdx;
            DWORD dwLibrary;
            DWORD dwGenre;
            DWORD dwMorphology;
            DWORD dwCategory;
        };
```

achPresetName Changes (SFe64)

- The \[20\] at the end is changed to \[256\].
    - This means that 256 characters can be used for a preset name instead of 20.

wPreset Changes

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
- It allows you to run GS(r) wide sounds alongside with the special velocity switching patches (Brand name: "MegaVoice(R)")on certain Yamaha(r) keyboards.

wBank Changes

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

"wPresetBagNdx" Changes (SFe64)

In SFe64, version 4, wPresetBagNdx is replaced with dwPresetBagNdx (a DWORD), in order to support a 32-bit number.

- This permits 4,294,967,296 items to be included in the "Preset Bag", increased from 65,536.

Old 2.04 fields "dwLibrary" and "dwGenre" are now defined.

- "dwLibrary" is for the overall name of the set of files contained in a library of SFe, version 4 files.
    - For example: "SFe Collection!" (with appropriate zero bytes)
- "dwGenre" is for the genre of music which the files are optimised for.
    - For example: "Rock" (with appropriate zero bytes)
- "dwMorphology" has been left out of this draft specification. It will eventually be re-introduced.

New field "dwCategory" (SFe64)

- This is a DWORD.
- This is for the category of instrument which the SF Version 4 file contains.
- For example: "Piano" (with appropriate zero bytes)

The last sfPresetHeader entry shouldn't need to be accessed, apart from the uses described in the SF2.04 specification.

This is a required sub-chunk. Files without a "phdr" sub-chunk are "Structurally Unsound".

* * *

## 7.3 "pbag" sub-chunk

This refers to the "Preset Bag" of the SFe file.

This sub-chunk is a multiple of 4 bytes (SFe32).

This sub-chunk is a multiple of 8 bytes (SFe64).

Its structure is this (SFe64):

```
struct sfPresetBag
        {
            DWORD dwGenNdx;
            DWORD dwModNdx;
        };
```

"wGenNdx" and "wModNdx" are now DWORD (SFe64)

- Up to 4,294,967,296 Generators and Modulators are therefore available in SFe64.
- Also renamed to "dwGenNdx" and "dwModNdx" to reflect the change from WORD to DWORD.

All values in this sub-chunk should be used as directed in the SF2.04 specification, with corrections owing to the changed data types.

This is a required sub-chunk. Files without a "pbag" sub-chunk are "Structurally Unsound".

* * *

## 7.4 "pmod" sub-chunk

The pmod sub-chunk is a multiple of 10 bytes, like in SF2.04. (SFe32)

The pmod sub-chunk is a multiple of 12 bytes. (SFe64)

Its structure is like this (SFe64):

```
struct sfModList
        {
            SFModulator sfModSrcOper;
            SFModulator sfModDestOper;
            LONG modAmount;
            SFModulator sfModAmtSrcOper;
            SFTransform sfModTransOper;
        };
```

The structure is very similar to SF2.04's PMod structure, with these differences:

- "modAmount" is now a LONG instead of a SHORT. (SFe64)
    - Since it is now a LONG, it permits the modulator amount to be up to 2,148,483,647.
- The SFModulator enum has some new options, which are listed elsewhere in this specification.
    - Legacy SF players which do not support these new enum options should ignore these new options.
    - This enum is 2 bytes in length.
- All other enums are 2 bytes in length.

This is a required sub-chunk. Files without a "pmod" sub-chunk are "Structurally Unsound".

* * *

## 7.5 "pgen" sub-chunk

The pgen sub-chunk is a multiple of 4 bytes, like in SF2.04.

Its structure is like this:

```
struct sfGenList
        {
            SFGenerator sfGenOper;
            genAmountType genAmount;
        };
```

And the types are defined like this:

```
typedef struct
        {
            BYTE byLo;
            BYTE byHi;
            BYTE by24;
            BYTE by32;
        } rangestype;
    
        typedef union
        {
            rangesType ranges;
            SHORT shAmount;
            LONG lngAmount;
            WORD wAmount;
            DWORD dwAmount;
        } genAmountType;
```

- The SFGenerator enum has some new options, which are listed elsewhere in this specification.
    - Legacy SF players which do not support these new enum options should ignore these new options.
    - This enum is 2 bytes in length.
- The GenAmount has obtained some new available data types.
    - Now, LONG and DWORD data types, represented by "lngAmount" and "dwAmount", can be used by modulators.
- Some new generators (generators which are new to this version), using a Signed value, may specify a 32-Bit Signed "LONG" value, represented by "lngAmount".
- Most existing generators, using Signed values, have now been upgraded to specify a 32-Bit Signed "LONG" value, represented by "lngAmount". (SFe64)
- Some new generators, using an Unsigned value, may specify a 32-Bit Unsigned "DWORD" value, represented by "dwAmount".
- Most existing generators, using Unsigned values, have now been upgraded to specify a 32-Bit Unsigned "DWORD" value, represented by "dwAmount". (SFe64)

This is a required sub-chunk. Files without a "pgen" sub-chunk are "Structurally Unsound".

* * *

## 7.6 "inst" sub-chunk

The inst sub-chunk is a multiple of 22 bytes. (SFe32)

The inst sub-chunk is a multiple of 260 bytes. (SFe64)

Its structure is like this (SFe64):

```
struct sfInst
        {
            CHAR achInstName[256];
            DWORD dwInstBagNdx;
        };
```

achInstName Changes (SFe64)

- The \[20\] at the end is changed to \[256\].
    - This means that 256 characters can be used for an instrument name instead of 20.

"wInstBagNdx" Changes (SFe64)

- In SFe64, version 4, wInstBagNdx is replaced with dwInstBagNdx (a DWORD), in order to support a 32-bit number.
- This permits 4,294,967,296 items to be included in the "Instrument Bag", increased from 65,536.
    - Therefore, the infamous "Out of Instrument Generators!" error should subside.

This is a required sub-chunk. Files without an "inst" sub-chunk are "Structurally Unsound".

* * *

## 7.7 "ibag" sub-chunk

This refers to the "Instrument Bag" of the SFe file.

This sub-chunk is a multiple of 4 bytes, like the pbag sub-chunk. (SFe32)

This sub-chunk is a multiple of 8 bytes, like the pbag sub-chunk. (SFe64)

Its structure is this (SFe64):

```
struct sfInstBag
        {
            DWORD dwInstGenNdx;
            DWORD dwInstModNdx;
        };
```

"wInstGenNdx" and "wInstModNdx" are now DWORD. (SFe64)

- Up to 4,294,967,296 Generators and Modulators are therefore available in SFe64.
    - Therefore, the infamous "Out of Instrument Generators!" error should subside.
- Also renamed to "dwInstGenNdx" and "dwInstModNdx" to reflect the change from WORD to DWORD.

All values in this sub-chunk should be used as directed in the SF2.04 specification, with corrections owing to the changed data types.

This is a required sub-chunk. Files without an "ibag" sub-chunk are "Structurally Unsound".

* * *

## 7.8 "imod" sub-chunk

The imod sub-chunk is a multiple of 10 bytes, like the pmod sub-chunk. (SFe32)

The imod sub-chunk is a multiple of 12 bytes, like the pmod sub-chunk. (SFe64)

Its structure is like this (SFe64):

```
struct sfModList
        {
            SFModulator sfModSrcOper;
            SFModulator sfModDestOper;	
            LONG modAmount;
            SFModulator sfModAmtSrcOper;
            SFTransform sfModTransOper;	
        };
```

The structure is very similar to SF2.04's imod structure, with these differences:

- "modAmount" is now a LONG instead of a SHORT. (SFe64)
    - Since it is now a LONG, it permits the modulator amount to be up to 2,148,483,647.
- The SFModulator enum has some new options, which are listed elsewhere in this specification.
    - Legacy SF players which do not support these new enum options should ignore these new options.
    - This enum is 2 bytes in length.
- The Preset Modulator values are added to the Instrument Modulator values, and that is the final modulator used.
- All other Enums are 2 bytes in length.

This is a required sub-chunk. Files without an imod sub-chunk are "Structurally Unsound".

* * *

## 7.9 "igen" sub-chunk

The igen sub-chunk is a multiple of 4 bytes, like the pgen sub-chunk.

Its structure is like this:

```
struct sfGenList
                {
                    SFGenerator sfGenOper;
                    genAmountType genAmount;
                };
```

And the types are defined like this:

```
typedef struct
        {
            BYTE byLo;
            BYTE byHi;
            BYTE by24;
            BYTE by32;
        } rangestype;
    
        typedef union
        {
            rangesType ranges;
            SHORT shAmount;
            LONG lngAmount;
            WORD wAmount;
            DWORD dwAmount;
        } genAmountType;
```

- The SFGenerator enum has some new options, which are listed elsewhere in this specification.
    - Legacy SF players which do not support these new enum options should ignore these new options.
    - This enum is 2 bytes in length.
- The GenAmount has obtained some new available data types.
    - Now, LONG and DWORD data types, represented by "lngAmount" and "dwAmount", can be used by modulators.
    - Some new generators (generators which are new to this version), using a Signed value, may specify a 32-bit Signed "LONG" value, represented by "lngAmount".
    - Most existing generators, using Signed values, have now been upgraded to specify a 32-bit Signed "LONG" value, represented by "lngAmount". (SFe64)
    - Some new generators, using an Unsigned value, may specify a 32-bit Unsigned "DWORD" value, represented by "dwAmount".
    - Most existing generators, using Unsigned values, have now been upgraded to specify a 32-bit Unsigned "DWORD" value, represented by "dwAmount". (SFe64)

This is a required sub-chunk. SFe files without an "igen" sub-chunk are "Structurally Unsound".

* * *

## 7.10 "shdr" sub-chunk

The shdr sub-chunk contains the headers for the sample data.

It is a multiple of 46 bytes (SFe32).

It is a multiple of 308 bytes (SFe64).

Its structure is like this (SFe64)**:**

```
struct sfSample
        {
            CHAR achSampleName[256]
            QWORD qwStart;
            QWORD qwEnd;
            QWORD qwStartloop;
            QWORD qwEndloop;
            QWORD qwSampleRate;
            BYTE byOriginalKey;
            CHAR chCorrection;
            QWORD qwSampleLink;
            SFSampleLink sfSampleType;	
        };
```

achSampleName Changes (SFe64)

- The \[20\] at the end is changed to \[256\].
    - This means that 256 characters can be used for an instrument name instead of 20.

All the DWORDs used in this sub-chunk have been changed to QWORDs. (SFe64)

Unlimited sample rate

- When reading version 4 files, if a sample rate of below 400 or above 50000 is encountered, no attempt should be made to change the sample rate.
- A zero sample rate should be reset.

Bit 4 of "sfSampleType" is reserved for Werner SF3 usage.

- Read the draft Werner SF3 specification for information!
- This specification is available at: [SoundFont3Format · FluidSynth/fluidsynth Wiki (github.com)](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format)

The "sfSampleType" enum is 2 bytes in length.

This is a required sub-chunk. Files without an "shdr" sub-chunk are "Structurally Unsound".

* * *

- If the sub-chunk sizes align with SF2/SFe32 in an SFe64 file, interpret the chunk as SFe32 data.
- If the sub-chunk sizes align with SFe64 in an SFe32 file, interpret the chunk as SFe64 data.
- If the sub-chunk sizes align with SFe64 in an SF2 file, or if the sub-chunk sizes do not align with either format, reject the file. It is "Structurally Unsound".