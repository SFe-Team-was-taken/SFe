# SF-enhanced (SFe) 4 specification

## Version 4.0.20241208b (Draft Specification) - 4.0.11 development

Copyright © 2020-2024 SFe Team and contributors

Based on the abandoned E-mu spec (Copyright © 1994–2002 E-mu Systems Inc.)

* * *

## 0.1 Revision history

|               |                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Revision      | Date                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| This version  | December 8, 2024     | Separated copyright/trademark and draft disclaimers <br> Rewritten 0.2 <br> Separated SFe team and special thanks lists <br> Corrected a name <br> Added and changed a few definitions <br> Added concept of RIFF-type format structures and rewrote 3.1 accordingly <br> Added clarification to 5.12.3 about tree structure <br> Defined new SFty value for 8-bit samples <br> Made it clear that a missing smpl sub-chunk without an SFty value that implies 8-bit samples means that a bank is Structurally Unsound <br> Added 6.2c <br> Added the SFe Compression 1.0 standard based on FluidSynth Werner SF3 August 2021 specification <br> Versioning update again <br> More consistent use of words and formatting                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| 4.0.10        | November 19, 2024    | Removed leading zeros in versioning <br> Updated license to be truly Open Source <br> SFty sub-chunk now required <br> Added SFvx and flag subchunks <br> Changed version planning <br> Removed references to new enum values for now (will be reintroduced in 4.1) <br> Added UTF-8 to isng <br> Removed info sub-chunk length limits <br> Updated structure in section 4 <br> Fixed a pronoun <br> Merged SFe32 and SFe64 into a single specification once again <br> Added section about chunk header types and long term support of SFe 4                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 4.0.9c        | November 16, 2024    | Updated SFe Team member listing                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 4.0.9b        | November 14, 2024    | Replaced wBank in a backwards-compatible manner to make it easier for developers to understand                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 4.0.9         | November 14, 2024    | Updated definitions of "case-insensitive" and "case-sensitive" to use UTF-8 instead of Ascii. <br> 7.2, 7.6 and 7.10 now use UTF-8 instead of ascii. <br> Changed wPreset to use the ISFe bank for implementation in 4.04. <br> Because the preset library management system values are DWORDs, reworking them for 4.05. <br> Added license <br> Re-added 9.7 from SF2.04 with updated information about implementation accuracy <br> Clarified incompatibility of cognitone-formatted banks <br> Changed format extensions <br> Changed ISFe-list sub-chunk to a list <br> Added SFty sub-chunk in ISFe-list sub-chunk                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 4.0.8         | October 30, 2024     | Started to fix SFe RIFF structure for 4.1-4.4 <br> Now consistent with WernerSF3 <br> Clarified versioning information                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 4.0.7c        | October 17, 2024     | Fixed some more things <br> Name update                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 4.0.7b        | October 12, 2024     | Updated program SFe32-to-SFe64 specification <br> Fix capitalisation in 1.5a <br> Remove extraneous table of contents entries <br> Fix more registered trademark symbols <br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 4.0.7         | October 10, 2024     | Table of contents added <br> Merge the pages into one <br> Fix the typos and formatting <br> Special thanks for spessasus for authoring these changes! <br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 4.0.6         | October 3, 2024      | Added milestone classification for some draft specifications in 0.1a  <br>Removed all SFe32-specific information, renamed to SFe64 spec  <br>Renamed 3.1a to 3.1, 6.1a to 6.1, 6.1b to 6.1a, 6.2a to 6.2, and 6.2b to 6.2a, for consistency  <br>Delayed modulator update to version 4.1  <br>Removed 7.1a, because it's not relevant to versions before 5.00  <br>Added LSB to example value in 10.1a  <br>Added more information about future plans  <br>Reworked SFe64 to be a simple 64-bit extension to SFe32 for now, features will come later                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 4.0.5c        | September 2, 2024    | Added clarification for timeframe in which 0.4 will be filled out  <br>Rewritten 1.1a to be clearer, moving links from 1.1b  <br>Removed redundant "important" words in 1.1b  <br>Moved some compatibility info from sections 1.3 and 3.1 to compatibility spec  <br>ROM samples no longer listed as deprecated in 3.2, 5.4, 5.5 and 6.1a  <br>Error handling plans for version 4.00.6 added in 3.3  <br>Fixed capitalisation in 4.5  <br>Added section 4.5a for file format extensions, removed .sf32 and .sf64  <br>Removed isfe reference for 5.1, SFe32 programs can determine WernerSF3 with wMajor=3  <br>Fixed reference to compatibility spec in 5.1a, compatibility spec is not used in SFe64  <br>Rewritten 5.2 to make it clearer, and to mention default modulator definitions for 4.01.  <br>Added heading 3 in formatting of section 7 and section 7.1a for subchunk size alignment.  <br>Removed reverb/chorus definitions in 8.1.2, 8.1.3 and 9.1.5 (will be restored in 4.1)  <br>Fixed some other typos and added a few other clarifications                                                                                                          |
| 4.0.5b        | September 1, 2024    | Clarified information about sample rates in section 7.10                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 4.0.5         | August 30, 2024      | All remaining SF32/SF64 references should now be renamed to SFe32/SFe64  <br>Added ROM sample specification for the AWE ROM emulator  <br>Replaced draft number references with the new versioning system  <br>Added clarification for the compatibility specification versioning  <br>Fixed mistake in INFO chunk information in the compatibility specification  <br>Clarified that this document is not created by E-mu  <br>Added placeholder for the SF Server link  <br>Specific version number added to title  <br>Added instructions to compatibility spec about how to handle incompatible compression  <br>Error messages modified to remove scom reference and fix version 3 reference to version 4  <br>Added section 1.5a to mention future plans for the SFe format  <br>Added 0.1a to describe specification versioning  <br>Removed unnecessary information about Creative Technology  <br>Proprietary compression formats are now forbidden in the program specification  <br>Added references to SFe Team; a list of developers can be found in 0.3a.  <br>Next version for release by early 2025 will have the SFe file repair program specification |
| 4.0.4         | July 4, 2024         | Clarified about legacy compliance and TSC in section 3.2.  <br>Added more clarification in revision history  <br>8-bit mode information updated again  <br>Added info about how SFe32 can be parsed as SFe64  <br>More information about the pdta structure added  <br>Real time synthesis is no longer mandatory  <br>Renamed to version 4 and updated versioning scheme  <br>Added preliminary Werner SF3 compatibility  <br>Removed scom sub-chunk  <br>For now, removed increased character limits in SFe32.  <br>Changed sleaf's name on the contact.  <br>Added information on bank select and TSC mode  <br>Added the isfe sub-chunk for SFe64  <br>One mention of "back and forth" now "bidirectional"  <br>Added and clarified some terms in glossary  <br>Stated that incompatible compression is no longer allowed in 6.1b.  <br>Renamed SF32 and SF64 to SFe32 and SFe64.  <br>Added clarification of "SFe format developers" in 1.5.  <br>Moved compatibility information to the compatibility specification.  <br>Added 5.1a to describe ifil sub-chunk versioning.                                                                                       |
| 4.0.3         | September 6, 2022    | Added clarification  <br>Renamed 32-bit SF version 3 to SF32  <br>Overall format has been renamed to SFe (SF enhanced)  <br>wBank bit 9 is no longer reserved.  <br>Silicon SF banks for SF64  <br>Added CM reset  <br>Changed isng value  <br>Fixed some pdta sub-chunks for SF64  <br>Corrected sfSampleType reference from bit 15 to bit 16.  <br>Renamed "back and forth" to "bidirectional"  <br>Changed "improved" to "fixed" in revision log  <br>Added a nicer diagram (can you find it?)  <br>Fixed extraneous reference to wBank2 in section 4.  <br>Modified information about the scom sub-chunk.  <br>8-bit mode information updated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 4.0.2         | July 22, 2022        | Renamed 64-bit SF3 to SF64 version 3  <br>32-bit SF3 is now 32-bit SF version 3  <br>Changed ASCII to UTF-8  <br>Fixed the wPreset and wBank (removed wBank2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 4.0.1         | April 12, 2020       | First version                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| (2.04a)       | (February 3, 2006)   | (The date listed in the specification title, different to value in 0.1 table in SF2.04)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| (2.04)        | (September 10, 2002) | (Last version authored by E-mu until format abandoned)                                                  


* * *

## 0.1a Specification Versioning

Final specifications have version numbers in the format x.yL, where x and y are numbers and l is a letter:

- x is incremented when a change in the SFe format is made in a way that makes the resulting files incompatible with the previous version.
- y is incremented when there are new features added to the SFe format.
- SFe should not skip "y" versions.
- L is incremented when there are small changes made to the specification. The first version will not include L.
- An example of a final specification version would be 4.0.

Draft specification milestones have version numbers in the format x.y.zL, where x, y and z are numbers and L is a letter. In this case, the versioning works similarly to a final specification, but with these changes:

- z is incremented when the draft undergoes a larger change, or large updates are made to the software.
- L is incremented when there are small changes, but only when pointed out by others. The first version will not include L.
- An example of a draft specification version would be 4.0.5.

During the development of specifications, version numbers will be in the format x.y.aaaabbccL, where x, y, z, a, b and c are numbers, and L is a letter. The versioning is similar to final specifications and milestone drafts, but aaaabbcc is the day in which the specification was updated, and L is incremented when updated.

The revision history table refers to development versions as "This version" and includes the cumulative changes made to the specification since the last milestone revision.

* * *

## 0.2 Copyright and Trademark Disclaimers

SoundFont® is a registered trademark of Creative Technology Ltd.

To avoid confusion with the official SoundFont standard, the file format is referred throughout to as "SF" and/or "SFe".

That being said, "soundfont" is rapidly becoming a genericised word via the actions of the VGM (video game music) and lightsaber communities. If you are a member of the VGM, lightsaber, or another community, by not appropriating "SoundFont" for your unrelated formats, you can help keep the meaning of the trademark.

Any excerpts from `SFSPEC24.PDF` are copyrighted by Creative Technology Ltd, and are only used for reference. However, we are confident that the base file format is not copyrightable.


* * *

## 0.2a License

Copyright © 2020-2024 SFe Team and contributors

Permission is granted to use, distribute and modify this draft specification for any use, provided that:

- this specification is clearly marked as a draft
- you attribute the SFe Team (do not remove copyright notices)
- you clearly mark any modifications that are made to the specification 
- you do not claim that we're affiliated with E-mu or Creative Labs.

For the benefit of the SFe community, please:

- share all modifications implemented in a program under this license
- do not remove the link to the latest version of the specification

The above guidelines are not required due to requirements listed by the Open Source Definition, but are good practice when redistributing the specification. 

This specification is provided "as-is" without any warranty.

* * *

## 0.2b Draft Disclaimer

This is a draft. Expect errors, and feel free to report them. Sylvia-leaf has access to a computer with a Sound Blaster X-Fi Titanium, so they will be able to test or reproduce any issues found on real hardware.

Do not use "draft" specifications (version number x.y.zL) to base final products on. Always refer to a "final" specification (version number x.yL).

* * *

## 0.3 Updates and comments

The website "soundfont.com" is dead (last archive.org snapshot we could found was 2012/13), and the provided email in `SFSPEC24.PDF` probably doesn't work, so contact the SFe Team:

- GitHub: https://github.com/SFe-Team-was-taken

A link to the SF Server Discord will be provided soon.

* * *

## 0.3a SFe Team

SFe Team members:

- sylvia-leaf (they/them) | Discord - @tanukilvia | Email - sylvialeaf6284@gmail.com
- Stgiga (they/them) | Discord - @stgiga
- spessasus
- davy7125

Want to join the SFe Team? Please contact sylvia-leaf using the contacts in section 0.3.

## 0.3b Special thanks to...

Thanks to these people for suggestions: derselbst, mawe42, sagamusix

* * *

## 0.4 Table of contents

<!-- Table of contents: contributed by @spessasus. -->
* [SF-enhanced (SFe) 4 specification](#sf-enhanced-sfe-4-specification)
  * [0.1 Revision history](#01-revision-history)
  * [0.1a Specification Versioning](#01a-specification-versioning)
  * [0.2 Copyright and Trademark Disclaimers](#02-copyright-and-trademark-disclaimers)
  * [0.2a License](#02a-license)
  * [0.2b Draft Disclaimer](#02b-draft-disclaimer)
  * [0.3 Updates and comments](#03-updates-and-comments)
  * [0.3a SFe Team](#03a-sfe-team)
  * [0.3b Special thanks to...](#03b-special-thanks-to)
  * [0.4 Table of contents](#04-table-of-contents)
  * [0.5 Illustrations](#05-illustrations)
* [Section 1: Introduction](#section-1-introduction)
  * [1.1a Scope and purpose of this document](#11a-scope-and-purpose-of-this-document)
  * [1.1b Important differences from the 2.04 document](#11b-important-differences-from-the-204-document)
  * [1.2 Document organisation](#12-document-organisation)
  * [1.3 SFe objectives](#13-sfe-objectives)
  * [1.4 The background of the SF format](#14-the-background-of-the-sf-format)
  * [1.5 Improvements and enhancements](#15-improvements-and-enhancements)
  * [1.5a Plans](#15a-plans)
  * [1.5b Long term support of SFe 4](#15b-long-term-support-of-sfe-4)
* [Section 2: Terms and abbreviations](#section-2-terms-and-abbreviations)
  * [2.1 Data structure terminology](#21-data-structure-terminology)
  * [2.2 Synthesis terminology](#22-synthesis-terminology)
  * [2.3 Parameter terminology](#23-parameter-terminology)
* [Section 3: RIFF-type format structure](#section-3-riff-type-format-structure)
  * [3.1 General RIFF-type format structures](#31-general-riff-type-format-structures)
  * [3.1a Chunk header types](#31a-chunk-header-types)
  * [3.2 Chunks and subchunks in SFe 4](#32-chunks-and-subchunks-in-sfe-4)
  * [3.3 Error handling](#33-error-handling)
* [Section 4: RIFF-type file format of SFe 4.0](#section-4-riff-type-file-format-of-sfe-40)
  * [4.1-4.4 File structure of SFe 4.0](#41-44-file-structure-of-sfe-40)
  * [4.5 Type definitions](#45-type-definitions)
  * [4.5a File format extensions](#45a-file-format-extensions)
* [Section 5: `info-list` chunk](#section-5-info-list-chunk)
  * [5.1 `ifil` subchunk](#51-ifil-subchunk)
  * [5.1a Versioning rules](#51a-versioning-rules)
  * [5.2 `isng` subchunk](#52-isng-subchunk)
  * [5.3 `INAM` subchunk](#53-inam-subchunk)
  * [5.4 `irom` subchunk](#54-irom-subchunk)
  * [5.5 `iver` subchunk](#55-iver-subchunk)
  * [5.6 `ICRD` subchunk](#56-icrd-subchunk)
  * [5.7 `IENG` subchunk](#57-ieng-subchunk)
  * [5.8 `IPRD` subchunk](#58-iprd-subchunk)
  * [5.9 `ICOP` subchunk](#59-icop-subchunk)
  * [5.10 `ICMT` subchunk](#510-icmt-subchunk)
  * [5.11 `ISFT` subchunk](#511-isft-subchunk)
  * [5.12 `ISFe-list` subchunk](#512-isfe-list-subchunk)
    * [5.12.1 `SFty` sub-chunk](#5121-sfty-sub-chunk)
    * [5.12.2 `SFvx` sub-chunk](#5122-sfvx-sub-chunk)
    * [5.12.3 `flag` sub-chunk](#5123-flag-sub-chunk)
* [Section 6: `sdta-list` chunk](#section-6-sdta-list-chunk)
  * [6.1a `smpl` sub-chunk](#61a-smpl-sub-chunk)
  * [6.1b SFe Compression](#61b-sfe-compression)
    * [6.1b.1 What is SFe Compression?](#61b1-what-is-sfe-compression)
    * [6.1b.2 File identification for SFe Compression](#61b2-file-identification-for-sfe-compression)
    * [6.1b.3 `sfSampleType` in `shdr` sub-chunk](#61b3-sfsampletype-in-shdr-sub-chunk)
    * [6.1b.4 Interpretation of sample data index fields in `shdr` sub-chunk](#61b4-interpretation-of-sample-data-index-fields-in-shdr-sub-chunk)
    * [6.1b.5 Using both compressed and uncompressed samples in the same file](#61b5-using-both-compressed-and-uncompressed-samples-in-the-same-file)
    * [6.1b.6 Unsupported features](#61b6-unsupported-features)
    * [6.1b.7 Proprietary compression formats](#61b7-proprietary-compression-formats)
  * [6.2a `sm24` and `sm32` sub-chunk](#62a-sm24-and-sm32-sub-chunk)
  * [6.2b Using 8-bit samples](#62b-using-8-bit-samples)
  * [6.2c Orphaned `sm24` and `sm32` sub-chunk(s)](#62c-orphaned-sm24-and-sm32-sub-chunks)
  * [6.3 Looping rules](#63-looping-rules)
* [Section 7: "pdta-list" chunk](#section-7-pdta-list-chunk)
  * [7.1 "Hydra" structure](#71-hydra-structure)
  * [7.2 `phdr` sub-chunk](#72-phdr-sub-chunk)
    * [`achPresetName` Changes](#achpresetname-changes)
    * [`wPreset` Changes](#wpreset-changes)
    * [New Bank System](#new-bank-system)
    * [Definitions of `dwLibrary` and `dwGenre`](#definitions-of-dwlibrary-and-dwgenre)
    * [Do not access the final `sfPresetHeader` entry](#do-not-access-the-final-sfpresetheader-entry)
  * [7.3 `pbag` sub-chunk](#73-pbag-sub-chunk)
  * [7.4 `pmod` sub-chunk](#74-pmod-sub-chunk)
  * [7.5 `pgen` sub-chunk](#75-pgen-sub-chunk)
  * [7.6 `inst` sub-chunk](#76-inst-sub-chunk)
    * [`achInstName` Changes](#achinstname-changes)
  * [7.7 `ibag` sub-chunk](#77-ibag-sub-chunk)
  * [7.8 `imod` sub-chunk](#78-imod-sub-chunk)
    * [New options for the `SFModulator` enum](#new-options-for-the-sfmodulator-enum-1)
    * [Preset and instrument modulators](#preset-and-instrument-modulators)
  * [7.9 `igen` sub-chunk](#79-igen-sub-chunk)
    * [New options for the SFGenerator enum](#new-options-for-the-sfgenerator-enum-1)
  * [7.10 `shdr` sub-chunk](#710-shdr-sub-chunk)
    * [`achSampleName` Changes](#achsamplename-changes)
    * [Sample Rate Limit Changes](#sample-rate-limit-changes)
    * [`sfSampleType` and SFe Compression](#sfsampletype-and-sfe-compression)
* [Section 8: Enumerators](#section-8-enumerators)
  * [8.1.1 Kinds of generator enums](#811-kinds-of-generator-enums)
  * [8.1.2/3 Generator enums definitions](#8123-generator-enums-definitions)
  * [8.2.1 Source enum controller palettes](#821-source-enum-controller-palettes)
  * [8.2.2-3 Source Directions and Polarities](#822-3-source-directions-and-polarities)
  * [8.2.4 Source Types](#824-source-types)
  * [8.3 Modulator transform enums](#83-modulator-transform-enums)
  * [8.4.1-4 Default modulators 1-4](#841-4-default-modulators-1-4)
  * [8.4.5-10 Default modulators 5-10](#845-10-default-modulators-5-10)
  * [8.5 Precedence, Absolute/Relative Values and Preset Level Availability of Generators.](#85-precedence-absoluterelative-values-and-preset-level-availability-of-generators)
* [Section 9: Parameters and synthesis model](#section-9-parameters-and-synthesis-model)
  * [9.1 SFe 4 synthesis model](#91-sfe-4-synthesis-model)
  * [9.1.1 Sample-based oscillator](#911-sample-based-oscillator)
  * [9.1.2 Sample looping](#912sample-looping)
  * [9.1.3 Filters](#913-filters)
  * [9.1.4 Final gain amplifier](#914-final-gain-amplifier)
  * [9.1.5 Effects Sends](#915-effects-sends)
  * [9.1.6 Low Frequency Oscillators (LFOs)](#916-low-frequency-oscillators-lfos)
  * [9.1.7 Envelope Generators](#917-envelope-generators)
  * [9.1.8 Modulation interconnection](#918-modulation-interconnection)
  * [9.2 MIDI functions](#92-midi-functions)
  * [9.3 Parameter units](#93-parameter-units)
  * [9.4 SF Generator Model](#94-sf-generator-model)
  * [9.5 SF Modulator Model](#95-sf-modulator-model)
  * [9.6 NRPN implementation](#96-nrpn-implementation)
  * [9.7 On implementation accuracy](#97-on-implementation-accuracy)
* [Section 10: Error-handling](#section-10-error-handling)
  * [10.1 Structural errors](#101-structural-errors)
  * [10.1a Duplicated preset locations within files](#101a-duplicated-preset-locations-within-files)
  * [10.1b Duplicated preset locations across files](#101b-duplicated-preset-locations-across-files)
  * [10.2 Undefined chunks](#102-undefined-chunks)
  * [10.3 Unknown Enumerators](#103-unknown-enumerators)
  * [10.4 Illegal Parameter Values](#104-illegal-parameter-values)
  * [10.5 Out of Range Values](#105-out-of-range-values)
  * [10.5a Exceeded Maximum File Size Limit](#105a-exceeded-maximum-file-size-limit)
  * [10.6 Missing Required Items](#106-missing-required-items)
  * [10.7 Illegal Enumerators](#107-illegal-enumerators)
* [Section 11: SiliconSFe](#section-11-siliconsfe)
* [Section 12: Glossary](#section-12-glossary)
<!-- End of TOC. -->

* * *

## 0.5 Illustrations

\[Again this is coming in a later draft.\]

# Section 1: Introduction

## 1.1a Scope and purpose of this document

- This is a draft specification for the SFe 4.0 file format, based on the famous E-mu Systems® SoundFont® 2.04, and Werner SF3 standards.
- It's intended to be a source of information on SFe.
- To create files that support SFe, you will need:
    - The SFe format, compatibility, and program specifications
    - E-mu's provided documents for legacy SF2.04 ([sfspec24.pdf](https://freepats.zenvoid.org/sf2/sfspec24.pdf))
    - The Werner SF3 specification ([draft by FluidSynth](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format)) - this will be integrated into SFe for 4.0.11 final release.
- All features from legacy SF2.04 will be retained.

* * *

## 1.1b Important differences from the 2.04 document

- This is not a standalone document; it refers to `SFSPEC24.PDF`. All relevant information from the Werner SF3 specification is included.
- This document is unofficial and was not created by E-mu. If you want this to be removed, we will remove it, but we hope that this is because you have your own update to the SF format ready.
- For copyright reasons, we cannot copy information from the original standard, except for what is required to interpret this document and what is allowed under fair use.

* * *

## 1.2 Document organisation

The sections in this specification map to `SFSPEC24.PDF`.

- Like `SFSPEC24.PDF`, section 1 and 2 gives introductory information about SFe.
- Sections 3–8 provide detailed information about the updates made to the SFe structure.
- Section 9 shows the synthesis engine.
- Section 10 describes any error handling that is necessary when opening SFe files.
- Section 11 describes legacy ROM methods of storing an SFe file.
- Section 12 is a glossary of most terms in this draft specification.

New sections may be added in the future, depending on if radical changes are made to the format.

* * *

## 1.3 SFe objectives

### The SFe standard has been created to provide a successor to E-mu Systems®'s SoundFont® 2.04 standard.

- The file size limit is 16 EiB.
- Large files (above 4 GiB) must use a 64-bit chunk header format.
- Programs that are designed to create existing SF2 files can easily be adapted to 64-bit with SFe.
- 64-bit headers will allow creators of sound banks to replace split banks with a large number of SF2 files (and supporting files like SFLISTs), with huge, single, ready-to-use files, where all samples and instruments can be shared in the sound bank's presets.
- SFe compatible players require a certain standard of features, which is in the separate program specification.

* * *

## 1.4 The background of the SF format

SoundFont® 1 refers to the proprietary version of the format used by the Creative Sound Blaster® AWE32 sound card released in 1994. It got one major feature update to version 1.5. 

- SoundFont® 1 files had a file extension of .SBK and cannot be used by many SF2.0x programs.
- This is the version used in the Creative DOS drivers.
- Creative is the brand name used by the company Creative Technology Ltd.
- As the specification for SF 1.x was never released, we don't know how SF 1.x files were structured.

Creative decided to release the specification to the public with version 2.00 in 1996 (specification date October 1995).

- This requires the Windows drivers for use in older Sound Blaster® cards.
- DOS drivers can only use .SBK (SoundFont® 1) files.

In 1998, modulators were added in the SoundFont® 2 version 2.01 (specification date August 1997).

- It is backwards compatible with 2.00.
- This was designed for use in the new SB Live! card (EMU10K1).

Finally, in 2005, version 2.04 was released with 24-bit support (specification date September 2002).

- It is backwards compatible with 2.01.
- This was designed for the SB X-Fi.

E-mu then abandoned the format. Creative Technology Ltd is still around, however, as a public company.

Current Creative Labs sound cards do not support the SoundFont® format; the Audigy RX from 2013 was the last model that supported the format. Newer cards, for instance, the AE-9, no longer use wavetable or MIDI sound synthesis.

At an unknown time, Kenneth Rundt, the author of SynthFont and a series of products based on it, added some custom features, mostly ported over from the DLS format:

- Always play the sample to the end
- Velocity to volume envelope attack (from DLS)
- Velocity to modulation envelope attack (from DLS)
- Vibrato lfo to volume (from DLS)

Werner Schweer found a way to compress SoundFont® 2 files (with the lossy Vorbis format) around 2010.

- The resulting format was known as SF3.
- It is commonly used by open source programs, such as MuseScore and FluidSynth.
- This is the reason why this format is not called .SF3 (it was in 4.0.1, but after **feedback by derselbst** and **mawe42** on GitHub, we changed it to SFe).
- SFe incorporates the Werner SF3 specification as SFe Compression.

Another development was done by Cognitone, which created an open source program that can losslessly compress SoundFont® 2 files (with FLAC). This was done in 2017.

- This was unofficially called SF4.
- This is intended to be the true version 4, as Cognitone SF4 seems to not have been as widespread as SF3.
- SF4 has also been rejected by FluidSynth as too loosely defined.

Finally, stgiga found out that many programs don't mind RIFF64 (RF64) files.

- RIFF64 files have a much larger size limit than 32-bit RIFF files.
- It gives us a new horizon to experiment with longer, higher quality samples.
- There are also many other advantages of the RIFF64 format.

This is where we stand right now.

* * *

## 1.5 Improvements and enhancements

SFe is designed for future improvements.

- These will be done in a more liberal way than the conservative manner of the SoundFont® 2 updates that E-mu has done.
- SFe is not affected by limitations created by the EMU8000 sound processor and Sound Blaster® cards, and therefore will have more improvements.
- Additionally, starting from SFe 5, SFe won't be affected by limitations created by legacy SF players.
- To avoid over-stress of developers of the SFe Team, as well as SFe instrument banks, features will be spread out across versions. We hope to release a new version every 3–5 years.

* * *

## 1.5a Plans

The features for SFe 4.0 have been frozen after the release of draft milestone 4.0.4. This doesn't mean that we're done with SFe, in fact, this is only the beginning of the format's development.

We decided to do a feature freeze for SFe 4.0 to make sure that SFe program developers have a reasonable set of features to implement. If we add too many features, it can overwhelm developers.

Here are a few things that are planned for SFe:

- Polyphone 3 will be the first program that supports SFe. It will use it by default with legacy SF being an option. (Polyphone 2.5 seems to be planned as an LTS release for legacy SF.)
- Negotiations with more SF program developers such as FluidSynth and Bassmidi will start soon.
- For SFe 4.1, there will be an overhaul of the default modulators system, inspired by the [DMOD proposal by spessasus](https://github.com/davy7125/polyphone/issues/205). Support for the related `PNMM` sub-chunk will also be included.
- A MIDI lyrics specification for MIDI players, along with Spessasus/Falcosoft RMIDI support, will become available in SFe 4.2.
- We will negotiate with the Synthfont author Kenneth Rundt about getting the Synthfont Custom Features added for SFe 4.2. Partial reverse engineering is currently underway to ensure that SFe features do not conflict with SFCF.

## 1.5b Long term support of SFe 4

SFe 4 is a "long-term support" version, and will get feature updates along with later versions such as SFe 5. While this is the case, some features are structurally incompatible with legacy SF2.04, and will not be available in SFe 5.

If an earlier major version of SFe is the main version used for a longer time than expected, then it can be declared as another LTS version. Such a LTS version will be declared in this section.

# Section 2: Terms and abbreviations

## 2.1 Data structure terminology

The data structure terminology used in SFe 4.0 is broadly the same as legacy SF2.04, with these additions:

- Branch - A subdivision of a tree strucutre containing either sub-branches or leaves that include values.
- BW64 - Broadcast Wave 64, used in the RF64 Header.
- Cognitone SF4 - An incompatible modification to Werner SF3 to allow support for FLAC audio compression. Because it is considered proprietary compression, usage is not allowed in SFe.
- Dynamic RIFF - A RIFF-type format by spessasus to allow formats to scale beyond 64-bit, while saving space. Implemented in future SFe versions. 
- FLAC - A lossless audio compression format commonly used in open-source software. Supported by Werner SF3, but not commonly used for that purpose.
- Leaf - A value found in a tree structure at the end of a branch.
- Lossless compression - Said of a compression format that retains all of its data when compressed. In terms of audio, there is no loss in quality in losslessly compressed audio.
- Lossy compression - Said of a compression format that does not retain all of its data when compressed. In terms of audio, there is a loss in quality in lossily compressed audio.
- OGG - See "Vorbis".
- Opus - A lossy audio compression format, slightly newer than OGG but with less wide adoption.
- Proprietary Compression - Any non-Werner SF3 SoundFont® compression system. Usage is not allowed in SFe.
- RF64 - See "RIFF64".
- RIFD - See "Dynamic RIFF".
- RIFF64 - A 64-bit RIFF-type format. Contrast to the RIFF format, which is 32-bit. Therefore, the maximum file size is above 4 gigabytes in size.
- RIFF-type format - Formats similar to RIFF (Resource Interchange File Format), see "RIFF" in `SFSPEC24.PDF` for more information.
- SFe - A family of enhancements to the SoundFont® 2.04 formats, unofficially created after E-mu/Creative abandoned the original format. May not be structurally compatible with legacy SF2.04.
- SFe 4 - This new specification, based on SoundFont® 2.04 and Werner SF3, with a set of new features making it more realistic. Not to be confused with the incompatible Cognitone SF4 file format.
- SFe-compatible - Indicates files, data, synthesisers, hardware or software that conform to the SFe specification.
- SFe Compression - The compression system based on Werner SF3 that SFe programs should be compliant with.
- Static RIFF - Any RIFF-type format with a fixed chunk size field width, including RIFF or RIFF64. See "RIFF-type format", "RIFF" and "RIFF64".
- Tree structure - A structure consisting of branches and leaves.
- Version 3 - See "Werner SF3".
- Version 4 - See "SFe 4".
- Vorbis - A lossy audio compression format commonly used in open-source software. The basic compression format that most Werner SF3 and SFe-compatible software should be expected to implement.
- Werner SF3 - A small upgrade to SoundFont® 2.04 created by Werner Schweer to allow an open source compression solution for SoundFont® programs. Standardised as SFe Compression.

And these changes:

- RIFF - The 32-bit static RIFF format used by SoundFont® 2.04 and the unmodified version of the format described by Microsoft in 1991.

* * *

## 2.2 Synthesis terminology

The synth terminology used in SFe 4.0 is broadly the same as legacy SF2.04, with these additions:

- AWE64 - The successor to the famous AWE32, adding features such as waveguide synthesis. Used the EMU8000 synthesizer chip, like the preceding AWE32. Available in "Value" or "Gold" versions.
- DAHDSR - Stands for Delay, attack, hold, decay, sustain, release. The six-step envelope system used in SF and SFe. 
- EMU10K1 - The successor to the EMU8000, designed by E-mu® for the Creative Labs SB Live!.
- EMU10K2 - An update to the EMU10K1, designed by E-mu® for the Creative Labs SB Audigy.
- EMU20K1 - The successor to the EMU10K2, designed by E-mu® for the Creative Labs SB X-Fi.
- EMU20K2 - An update to the EMU20K1, please refer [here](https://en.wikipedia.org/wiki/Sound_Blaster_X-Fi) for information on SB X-Fi cards that include it.
- Hold - The portion of the DAHDSR envelope after the attack portion, but before the decay portion starts.
- Legacy sound card - A Sound Blaster® (or other sound card) that uses a hardware MIDI synthesiser capable of using banks in the SoundFont® format.
- ROM samples - Obsolete feature used in legacy sound cards, most modern SF2 files do not use this feature.
- Sharp - Said of a tone that is higher in pitch than another reference tone.
- SB - Abbreviation of "Sound Blaster®". For example, "SB X-Fi".
- Sound Blaster® Live! - The successor to the AWE64, which improved the synthesizer chip to the EMU10K1, supporting modulators.
- Sound Blaster® Audigy - The successor to the SB Live!, containing the EMU10K2 chip.
- Sound Blaster® X-Fi - The successor to the SB Audigy, containing the EMU20K1 or EMU20K2 chip. Supports 24-Bit SoundFont® 2 files (2.04).
- Synth - Abbreviation of "Synthesiser," see "Synthesiser" in `SFSPEC24.PDF` for more information.


These changes:

- Articulation - Modulation of available parameters and usage of extra samples to produce expressive musical notes.
- Case-insensitive - Indicates that a UTF-8 character or string treats alphabetic characters of upper or lower case as identical.
- Case-sensitive - Indicates that a UTF-8 character or string treats alphabetic characters of upper or lower case as distinct.
- Downloadable - legacy SF2.0x, Werner SF3 or SFe file obtained from the internet. (Old meaning referred to the obsolete ROM system)
- MIDI Bank - Groups of up to 128 presets, which can be selected by the two MIDI "Bank Select" control changes (CC00 and CC32).

And these removals:

- Preditor (refers to an old legacy SF2.0x editor made by E-mu)

* * *

## 2.3 Parameter terminology

The parameter terminology used in SFe 4.0 is broadly the same as legacy SF2.04, with these additions:

- Amplification - An increase in volume or amplitude of a signal.
- Flat - Said of a tone that is lower in pitch than another reference tone.

# Section 3: RIFF-type format structure

## 3.1 General RIFF-type format structures

RIFF-type formats are the file format used in legacy SF2.04, Werner SF3 and SFe standards. There are a few different RIFF-type format structures:

- RIFF is the basic version with 32-bit chunk headers, and is used in legacy SF2.04 and Werner SF3.
- RIFF64 (also called RF64) is mostly compatible with RIFF, but uses 64-bit chunk headers.
- RIFX is a big-endian version of 32-bit RIFF, while RIFF and RIFF64 are little-endian formats.
- RIFD is the dynamic version of RIFF developed by spessasus. It will be included in a future version of SFe.

RIFF-type formats are created in building blocks known as "chunks."

Chunks are defined using this structure:

- A unique four character code (FourCC), listed above.
- `ckID`: type of data in chunk
- `ckSize`: size of chunk (RIFF, RIFX), equal to 4,294,967,295 (RIFF64)
- `ds64`: size of chunk (RIFF64 only)
- `ckDATA[ckSize]`: the data inside the chunks, including pad bytes.

Chunks can be further divided into "sub-chunks."

Orders of chunks in all SF files are strictly defined, as in versions 2 and 3, and should be kept to, except for TSC mode.

## 3.1a Chunk header types

In SFe, there are different chunk header types that are used in the format. These correspond to different RIFF-type formats. Currently, there are two defined chunk header types:

- 32-bit static
    - This is the same as legacy SF
    - This corresponds to RIFF.
    - The FourCC used is `RIFF`.
- 64-bit static
    - A `ds64` chunk is added
    - The FourCC used is `RF64`.
    - To prevent loading by incompatible players, the `sfbk` fourcc is replaced with `sfen` (**SF**-**en**hanced)
    - This corresponds to RIFF64.

Future versions of SFe may define different chunk header types. In particular, we are planning on introducing a header type called "Dynamic", which uses the `RIFD` FourCC, and allows scaling of chunk sizes beyond 64-bit while saving space for banks that don't use the full 64 bits (which is currently every bank).

* * *

## 3.2 Chunks and subchunks in SFe 4

Like legacy SF2.04, there are 3 main chunks:

1.  `INFO-list` Chunk: contains important information about the soundfont.
2.  `sdta-list` Chunk: A single sub-chunk containing audio samples.
3.  `pdta-list` Chunk: Nine sub-chunks (in the "Hydra" structure, named after a many-headed beast) containing the parameters about how the audio samples should be played. (According to E-mu, the hydra has nine heads. Cut one off, and another two grow.)

The three main chunks should appear in this order, and the nine sub-chunks of the `pdta-list` chunk should appear in the order described.

* * *

## 3.3 Error handling

RIFF-type formats have error checking features about:

- The size of the file
- The length of the chunks
- The length of the sub-chunks

Using this information, it is possible to check for damage to an SF(e) file:

- If any damage is detected due to such a mismatch, the file should be rejected as "Structurally Unsound."
- Like E-mu® SoundFont® 2.x and Werner SF3, developers can create programs which correct "Structurally Unsound" SFe banks.
- Please refer to the File Repair Specification for help on how to create such a program.

# Section 4: RIFF-type file format of SFe 4.0

## 4.1-4.4 File structure of SFe 4.0

This is the structure of a file with 64-bit chunk header. We will rework this file structure using a similar four-level structure as the original `SFSPEC24.PDF`, as that makes it easier to format the many different header structures.

```c
RF64('sfen'
    {
    ds64(dataSize)
    LIST('INFO'
            {
                ifil(
                    struct sfVersionTag 
                    {
                        WORD wMajor;
                        WORD wMinor;
                    }
                );
                isng(szSoundEngine:ZSTR);
                irom(szROM:ZSTR);
                iver(
                    struct sfVersionTag 
                    {
                        WORD wMajor;
                        WORD wMinor;
                    }
                );
                ICRD(szDate:ZSTR);
                IENG(szName:ZSTR);
                IPRD(szProduct:ZSTR);
                ICOP(szCopyright:ZSTR);
                ICMT(szComment:ZSTR);
                ISFT(szTools:ZSTR);
                LIST('ISFe'
                    {
                        SFty(szSFeType:ZSTR);
                        SFvx(
                            struct SFeExtendedVersion
                            {
                                WORD wSFeSpecMajorVersion;
                                WORD wSFeSpecMinorVersion;
                                CHAR achSFeSpecType[20];
                                WORD wSFeDraftMilestone;
                                CHAR achSFeFullVersion[20];
                            };
                        );                            
                        flag(
                            struct SFeFeatureFlag
                            {
                                BYTE byBranch;
                                BYTE byLeaf;
                                DWORD dwFlags;
                            };
                        );
                        prsw(
                            // Not defined until 4.3
                        );
                    }
                );
            }
        )
    LIST('sdta'
            {
                smpl(<sample:SHORT>);
            }
            {
                sm24(<sample:BYTE>);
            }
            {
                sm32(<sample:BYTE>);
            }
        )
    LIST('pdta'
            {
            phdr(
                struct sfPresetHeader
                    {
                        CHAR achPresetName[20];
                        WORD wPreset;
                        BYTE byBankMSB;
                        BYTE byBankLSB;
                        WORD wPresetBagNdx;
                        DWORD dwLibrary;
                        DWORD dwGenre;
                        DWORD dwMorphology;
                    }
                );
                pbag(
                    struct sfPresetBag
                    {
                        WORD wGenNdx;
                        WORD wModNdx;
                    }
                );
                pmod(
                    struct sfModList
                    {
                        SFModulator sfModSrcOper;
                        SFGenerator sfModDestOper;
                        SHORT modAmount;
                        SFModulator sfModAmtSrcOper;
                        SFTransform sfModTransOper;
                    }
                );
                pgen(
                    struct sfGenList
                    {
                        SFGenerator sfGenOper;
                        genAmountType genAmount;
                    }
                );
                inst(
                    struct sfInst
                    {
                        CHAR achInstName[20];
                        WORD wInstBagNdx;
                    }
                );
                ibag(
                    struct sfInstBag
                    {
                        WORD wInstGenNdx;
                        WORD wInstModNdx;
                    }
                );
                imod(
                    struct sfInstModList
                    {
                        SFModulator sfModSrcOper;
                        SFGenerator sfModDestOper;
                        SHORT modAmount;
                        SFModulator sfModAmtSrcOper;
                        SFTransform sfModTransOper;
                    }
                );
                igen(
                    struct sfInstGenList
                    {
                        SFGenerator sfGenOper;
                        genAmountType genAmount;
                    }
                );
                shdr(
                    struct sfSample
                    {
                        CHAR achSampleName[20];
                        DWORD dwStart;
                        DWORD dwEnd;
                        DWORD dwStartloop;
                        DWORD dwEndloop;
                        DWORD dwSampleRate;
                        BYTE byOriginalKey;
                        CHAR chCorrection;
                        WORD wSampleLink;
                        SFSampleLink sfSampleType;
                    }
                );
            }
        )
    }
)
```

* * *

## 4.5 Type definitions

The type definitions are identical to those used in legacy SF2.04.

* * *

## 4.5a File format extensions

The file format extension to use for SFe files is generally `.sft`. `.sf4` is avoided due to incompatibility with cognitone formatted banks.

When opening a bank with extension `.sft`, programs must determine the correct version to use. The `ifil` value and `ISFe-list` sub-chunk provide hints.

# Section 5: `info-list` chunk

## 5.1 `ifil` subchunk

The value of this subchunk **must** match the values found in the `SFvx` subchunk. If there is a mismatch, the value of `ifil` prevails. 

The size must be exactly four bytes. Reject files with an `ifil` subchunk that isn't four bytes as "Structurally Unsound."

If the `ifil` subchunk is missing, either:

- Assume version 4.0.
- Reject the file as "Structurally Unsound."

* * *

## 5.1a Versioning rules

In SFe 4.0, new versioning rules are used to replace the old ones.

The value of `wMajor` increases every time a change is made to the format that makes it incompatible with existing players.

- There will be at least 6 months between the first draft milestone of a new `wMajor` version and the release of the final specification.
- Older `wMajor` versions must be supported, either directly or via translation to the latest version.
- We strive to minimize the number of these updates whenever possible in favor of updates that are backward compatible.

The value of `wMinor` increases every time a change is made to the format while retaining backwards compatibility.

- These updates generally have only one or two draft milestones before the final specification releases.
- Feature updates in these versions are smaller.

The specification type used is found in the `ISFe-list` sub-chunk.

* * *

## 5.2 `isng` subchunk

A new default isng sub-chunk value is used in SFe: `SFe 4`.

- SFe 4.0 players should recognize this and remove the default velocity related filter used in legacy SF2.04.
- The ten "Default Modulators" will also be disabled by default. The Default modulation definition will be added in SFe 4.1.
- In the case of a missing isng chunk, files with an ifil sub-chunk with `wMajor` = `2` or `3` and `wMinor` >= `1024`, or `wMajor` >= `4`, assume an isng sub-chunk value of `SFe 4`. Don't assume `EMU8000`.

Additionally, UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `isng` subchunk contains a UTF-8 string of any length.
- Example of value: `SFe 4` (with appropriate zero bytes).

Reject anything not terminated with a zero byte, and assume the value `SFe 4`. Do NOT assume `EMU8000` by default.

* * *

## 5.3 `INAM` subchunk

This is mostly the same as in legacy SF2.04, but UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `INAM` subchunk contains a UTF-8 string of any length.
- Example of value: `GM Sound Set` (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.4 `irom` subchunk

- Read the legacy SF2.04 specification for info on how to use ROM samples.
- The ROM emulator should be implemented in SFe programs.
- This subchunk may eventually be reused for other features in a future version of this specification.

* * *

## 5.5 `iver` subchunk

- Read the legacy SF2.04 specification for info on how to use ROM samples.
- The ROM emulator should be implemented in SFe programs.
- This subchunk may eventually be reused for other features in a future version of this specification.

* * *

## 5.6 `ICRD` subchunk

This is mostly the same as in legacy SF2.04, but UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `ICRD` subchunk contains a UTF-8 string of any length.
- Example of value: `December 8, 2024` (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.7 `IENG` subchunk

This is mostly the same as in legacy SF2.04, but UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `IENG` subchunk contains a UTF-8 string of any length.
- Example of value: `SF Author` (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.8 `IPRD` subchunk

This is mostly the same as in legacy SF2.04, but UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `IPRD` subchunk contains a UTF-8 string of any length.
- Example of value: `SFe Players` (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.9 `ICOP` subchunk

This is mostly the same as in legacy SF2.04, but UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `ICOP` subchunk contains a UTF-8 string of any length.
- Example of value: `Copyright © All Rights Reserved.` (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.10 `ICMT` subchunk

This is mostly the same as in legacy SF2.04, but UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `ICMT` subchunk contains a UTF-8 string of any length.
- Example of value: `This file contains 128 instruments and a drum kit.` (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.11 `ISFT` subchunk

This is mostly the same as in legacy SF2.04, but UTF-8 is now used instead of ASCII, and the length limit is removed.

- The `ISFT` subchunk contains a UTF-8 string of any length.
- Example of value: `SFe Editor version 4.0` (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.12 `ISFe-list` subchunk

The `ISFe-list` sub-chunk includes many different sub-chunks to show information about SFe-specific features. Generally, we use the `ISFe-list` sub-chunk to make it clearer that this kind of information is SFe-specific.

Due to compatibility constraints, the `ISFe-list` sub-chunk is found inside the `INFO-list` subchunk, rather than as a fourth RIFF chunk. Legacy SF players may not support more than three main RIFF chunks. If we can't use list sub-chunks inside other chunks, then instead of an SFe sub-chunk, the sub-chunks defined here will just be part of the `INFO-list` subchunk until SFe 5 is released, which will include a fourth separate `ISFe-list` chunk.

### 5.12.1 `SFty` sub-chunk

The `SFty` sub-chunk is a required sub-chunk identifying the variant of SFe the bank is formatted in. It contains a UTF-8 string of 256 or fewer bytes including one or two terminators of value zero to make the total byte count even.

The `SFty` string is used by SFe-compatible players to assist in loading banks by telling the program what variant of SFe to load a bank as.

The defined values of the `SFty` chunk are:

- the 12 bytes representing `SFe-static` as 10 UTF-8 characters followed by two zero bytes.
- the 20 bytes representing `SFe-static with TSC` as 19 UTF-8 characters followed by one zero byte.
- the 20 bytes representing `SFe-static (8-bit)` as 18 UTF-8 characters followed by two zero bytes.
- the 28 bytes representing `SFe-static (8-bit) with TSC` as 27 UTF-8 characters followed by one zero byte.

The field should conventionally never be longer than 28 bytes.

The UTF-8 should be treated as case-sensitive. In other words, `sfe-static with tsc` is not the same as `SFe-static with TSC`.

If the SFty sub-chunk is missing, not terminated in a zero-valued byte, or its contents are an undefined value, other properties of the structure should be used to determine the variant of SFe that is in use. Do not assume `SFe-static`; only use such a value when it is evident beyond a reasonable doubt that the file used is SFe.

### 5.12.2 `SFvx` sub-chunk

The `SFvx` sub-chunk is a required sub-chunk identifying any extended SFe version attributes. It is always 46 bytes in length, and contains data according to the structure:

```c
struct SFeExtendedVersion
{
    WORD wSFeSpecMajorVersion;
    WORD wSFeSpecMinorVersion;
    CHAR achSFeSpecType[20];
    WORD wSFeDraftMilestone;
    CHAR achSFeFullVersion[20];
};
```

The `WORD` values `wSFeSpecMajorVersion` and `wSFeSpecMinorVersion` contain the SFe specification version. This can be used by players for any purpose.

The UTF-8 character field `achSFeSpecType` contains the specification type expressed in UTF-8. It must be a defined value, but implementations may define custom values for internal purposes. For the purposes of SFe, the defined values are:

- `Final` for final specifications.
- `Milestone` for draft specification milestones.
- `Dev` for rolling draft specifications.

The UTF-8 should be treated as case-sensitive. In other words, `final` is not the same as `Final`. If the contents of `achSFeSpecType` are an undefined value, the field should be ignored and `Final` assumed.

The `WORD` value `wSFeDraftMilestone` contains the draft specification milestone that a bank was created to. This varies depending on the value of achSFeSpecType:

- If a bank is created to a final specification `4.0`, then `achSFeSpecType=Final`, `wSFeDraftMilestone=0`. It is safe to ignore the value of `wSFeDraftMilestone`, but you should write the value as zero.
- If a bank is created to draft specification milestone `4.0.10`, then `achSFeSpecType=Milestone`, `wSFeDraftMilestone=10`.
- If a bank is created to a rolling specification created after `4.0.10` but before `4.0.11`, then `achSFeSpecType=Dev`, `wSFeDraftMilestone=11`.

The UTF-8 character field `achSFeFullVersion` contains the full version string of the specification used, for example `4.0`, `4.0.10` or `4.0.yyyymmddx`.

If the `SFvx` sub-chunk is missing, or its size is not 46 bytes, the field should be ignored and these values assumed:

- `wSFeSpecMajorVersion` and `wSFeSpecMinorVersion` correspond to the highest version declared in the `flag` sub-chunk
    - If there is no valid `flag` sub-chunk, then assume the highest SFe version supported by the program.
- `achSFeSpecType=Final`
- `wSFeDraftMilestone=0`
- `achSFeFullVersion` corresponds to the other assumed values

The file may optionally be rejected as Structurally Unsound.

### 5.12.3 `flag` sub-chunk

The `flag` sub-chunk is a required sub-chunk identifying the feature flags used by a bank. It is always a multiple of 6 bytes in length, and contains a minimum of two records, one for a feature flag and another for a terminal record according to the structure:

```c
struct SFeFeatureFlag
{
    BYTE byBranch;
    BYTE byLeaf;
    DWORD dwFlags;
};
```

The `BYTE` value `byBranch` represents the branch of the feature. Branches correspond to types of features.

The `BYTE` value `byLeaf` represents the leaf of the feature. Leaves correspond to specific features. 

The `DWORD` value `dwFlags` represents the feature flags themselves, which represent different parts of the feature. Depending on the `byLeaf` value, it can be a number, a series of bytes, etc.

A tree value is a combination of a branch value and a leaf value, and is conventionally written in the format `[branch]:[leaf]` with hexadecimal values, for example "feature flag 03:01" refers to the feature flag with branch number `3` and leaf number `1` (SFe Compression sample compression formats). While the `flag` sub-chunk uses a tree structure, it should be noted that no branch includes sub-branches; the branches only include leaves.

Branch numbers between `240` (`F0`) and `255` (`FF`) are private-use branches that will not be defined in the SFe specification itself, and are free to be used by programs.

An exhaustive list of feature flags and their corresponding tree values can be found in the compatibility specification. This will update with each SFe version.

The terminal record should never be accessed in normal usage, but its value of `byBranch` and `byLeaf` have strict values depending on the specification version. Any records after the terminal record or with a higher tree value combination (except for the defined private-use area) should be ignored.

If the `flag` subchunk is missing, or its size is not a multiple of 6 bytes, then an effort should be made to recover the data. If data is not recoverable, then it can be rebuilt from the properties of the data in the rest of the bank. Do not reject the file as Structurally Unsound. 

* * *

&nbsp;

# Section 6: `sdta-list` chunk

## 6.1a `smpl` sub-chunk

This sub-chunk should now be present in SFe files, as currently, there is no ROM where samples can be read from. This does not include AWE ROM emulation.

- This contains one or more samples of audio in linearly coded 16-bit, signed, little endian words.
- No more leeway of 46 zero-valued samples is required after each sample.
- Before saving, SFe editors should insert this leeway. Otherwise, they might give a warning telling the user that loop and interpolation quality may be affected.
- If ROM samples are detected in SFe files, attempt to load them, even if this sub-chunk is missing.
- If this sub-chunk is missing, and no ROM samples are found, show an error message as mentioned in the program specification.

* * *

## 6.1b SFe Compression

To implement compression in your SFe bank, please use the SFe Compression specification, listed in this section (6.1b).

### 6.1b.1 What is SFe Compression?

SFe Compression is the compression encoding system used by SFe, based on the earlier [Werner SF3](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format) system widely used by the open source community.

By standardising on Werner SF3 in the form of SFe Compression, we will hopefully ensure that everyone uses the same compression formats. Due to this, we will only make small changes to SFe Compression which correspond to updates to the Werner SF3 specification by other SF player programs. To achieve this, all SFe players should implement SFe Compression.

### 6.1b.2 File identification for SFe Compression

The `wMajor` value in the `ifil` sub-chunk is set to `3` instead of `2`. The value of the `SFvx` sub-chunk remains unchanged. Therefore, SFe players should not use the `ifil` value to determine the SFe version, but rather the `SFvx` sub-chunk.

### 6.1b.3 `sfSampleType` in `shdr` sub-chunk

Bit 4 of the `sfSampleType` field indicates a sample that has received some kind of compression. While most Werner SF3 compatible programs compress the samples using the Vorbis format, it cannot be assumed. SFe players must determine the encoding that is used for each sample. 

For a sample to be valid:
- the type of compression and/or encoding must be recognised and supported by the program.
- the compression and/or encoding format must be valid.
- the compressed sample must only have one channel.

A sample is not valid if any of these conditions are not true. If a sample is not valid, then all instruments and presets that use the sample should be rejected.

### 6.1b.4 Interpretation of sample data index fields in `shdr` sub-chunk

If bit 4 of the `sfSampleType` field is set, then the interpretation of the four sample data index fields changes:

- `dwStart` points to the first byte of the compressed byte stream relative to the beginning of the `smpl` sub-chunk.
- `dwEnd` points to the last byte of the compressed byte stream, instead of the first zero-valued sample data point after the sample data in legacy SF2.04.
- `dwStartLoop` and `dwEndLoop` specify loop points relative to the start of the individual uncompressed sample data, in sample data points.

If bit 4 of the `sfSampleType` field is clear, then the sample data index fields should be interpreted as in legacy SF2.04.

### 6.1b.5 Using both compressed and uncompressed samples in the same file

You can use both compressed and uncompressed samples with SFe Compression. Simply place uncompressed PCM samples at the beginning of the `smpl` sub-chunk before the compressed sample byte stream. Because each sample is compressed individually, the resulting byte streams of all encoded samples are written to the `smpl` sub-chunk. The `smpl` sub-chunk may also contain uncompressed little-endian PCM samples.

For compressed byte streams, it is not necessary to add fourty-six zero-valued sample data points after each sample. The length of the `smpl` sub-chunk is not required to be a multiple of two for compressed banks, and its surrounding `LIST` chunk is also not padded to a multiple of two as a consequence.

### 6.1b.6 Unsupported features

Compressed samples are always 16-bit samples. They do not make use of the `sm24` (or `sm32`) sub-chunk. If an `sm24` sub-chunk is present, its respective byte counterparts to the compressed byte stream stored in the `smpl` sub-chunk remain unused. Since all uncompressed PCM samples are stored before compressed samples in the `smpl` sub-chunk, the size of the `sm24` sub-chunk is minimised. The `sm24` size constraint defined in legacy SF2.04 therefore no longer applies in compressed banks.

Sample links are not used in banks compressed with SFe Compression. The value of `wSampleLink` should be read and written as zero. 

The "scom" sub-chunk found in draft milestones 4.0.3 and earlier is now obsolete. Do not use this sub-chunk in SFe 4.

### 6.1b.7 Proprietary compression formats

The only supported compression system for SFe is the Werner SF3-compatible SFe Compression. Proprietary SF compression formats (.sfark, .sfpack, .sf2pack, .sfogg, .sfq, Cognitone SF4) must not be used. Because Cognitone SF4-formatted banks are not valid Werner SF3 banks, they are also incompatible with SFe Compression.

* * *

## 6.2a `sm24` and `sm32` sub-chunk

These sub-chunks are optional.

- The `sm32` sub-chunk contains the least significant byte, and the `sm24` sub-chunk contains the next least significant byte after sm32.
- Each sub-chunk is exactly half the size of the `smpl` sub-chunk for uncompressed banks. This may not apply when SFe Compression is in use.
- For every two bytes in the `smpl` sub-chunk, there is one byte in these sub-chunks.
- Compressed banks are limited to 16-bit samples. This limitation may be removed in future versions of SFe.

[Figure]

If these sub-chunks are present, they are combined with the other sub-chunks to create a sample with higher bitdepth.

- If the `ifil` version is below `2.04` (signifying legacy SF2.01 or earlier), both `sm24` and `sm32` are ignored.
- If the `ifil` version is exactly `2.04` (signifying legacy SF2.04), only `sm32` is ignored. The `sm24` sub-chunk is still used.
- For uncompressed banks, these sub-chunks are not exactly half the size of the `smpl` sub-chunk (or otherwise invalid), the data should be ignored.
- If only the `sm32` sub-chunk is invalid, the `sm24` sub-chunk should still be loaded.
- However, if only the `sm24` sub-chunk is invalid, both sub-chunks should be ignored.
- If the `sm24` sub-chunk is ignored, the synthesizer should only attempt to render the first 16 bits of the samples contained within the `smpl` sub-chunk.
- If only the `sm32` sub-chunk is ignored, the synthesizer should attempt to render both the `smpl` and `sm24` sub-chunks, resulting in a 24-bit sample.
- We recommend only using `sm32` with 64-bit chunk headers. Using `sm32` with a 32-bit chunk header is syntactically valid, but it is not practical due to file size limitations.

* * *

## 6.2b Using 8-bit samples

If the smpl sub-chunk is missing, but the `sm24` or `sm32` sub-chunks are present, then the `sm24` or `sm32` sub-chunk is considered "orphaned". 

In this case, the value of the `SFty` sub-chunk inside the `ISFe-list` sub-chunk should be checked. If it is equal to `SFe-static (8-bit)` or `SFe-static (8-bit) with TSC`, then 8-bit sample mode is to be activated.

- The sample depth is eight bits.
- The length of the `sm24` sub-chunk should be rounded up to the nearest byte, as if the sub-chunk was being used with a `smpl` sub-chunk.
- This mode can only be used if all samples are 8-bit. You cannot mix 8-bit and higher sample depths.
- SFe 4 does not support non-standard sample bit depths (6-bit, 12-bit, 18-bit, etc.)

If there is an orphaned `sm24` or `sm32` sub-chunk, and the `SFty` sub-chunk is missing or is not equal to a value that corresponds to 8-bit samples being present, then the file should be rejected as Structurally Unsound. 

## 6.2c Orphaned `sm24` and `sm32` sub-chunk(s)

If somehow, you've got both a `sm24` and a `sm32` sub-chunk, but no `smpl` sub-chunk, the `sm24` sub-chunk is the most significant byte, and 16-bit sample playback is assumed. Editing software should give a warning if there is a `sm24` and a `sm32` sub-chunk but no `smpl` sub-chunk, and should convert it to a 2.01-compliant 16-bit format.

This behaviour should be followed if supported, regardless of whether 8-bit sample playback support is actually supported.

* * *

## 6.3 Looping rules

- No more leeway of eight samples is required.
- Before saving, SFe editors might give a warning about this leeway telling the user that loop and interpolation quality may be affected.

# Section 7: `pdta-list` chunk

## 7.1 "Hydra" structure

Like in legacy SF2.04, the format SFe 4.0 is based on, the structure used is known as the "hydra" structure.

According to E-mu Systems®, a hydra has nine heads. Cut one off, and another two grow.

No major changes have been made to the structure itself. All nine of the sub-chunks are required. If any are missing, the file is "Structurally Unsound."

* * *

## 7.2 `phdr` sub-chunk

The size of this chunk is a multiple of 38 bytes.

Its structure is the same as in legacy SF2.04.

### `achPresetName` Changes

- In legacy SF2.04, `achPresetName` must be an ASCII string.
- Now, UTF-8 replaces ASCII, allowing more characters to be written.

### `wPreset` Changes

- In legacy SF2.04, bits 2–8 were used to select up to 128 instruments. Bits 1 and 9–16 were unused.
- Bits 10–16 will be usable to select alternate banks using the `ISFe-list` subchunk, starting with SFe 4.3.
- It's designed to be used with sysex or other commands corresponding to General MIDI extension resets.
- What bits 9–16 do in SFe 4.0:
    - Bit 9 remains reserved.
    - Bits 10-16 are reserved for MIDI commands as defined in the `ISFe-list` subchunk. For now, these bits should be written as clear.
- It allows you to run multiple standards that may conflict with each other.

### New Bank System

In legacy SF2.04, only one MIDI Bank Select could be used (typically MSB).

- SFe draft specification milestone 4.0.1 had a field called `wBank2`. Any draft with `wBank2` is now obsolete.
- We commend E-mu for being forward enough thinking to not use a `BYTE` for bank selection.
- In legacy SF2.04 and 4.0.1, bit 1 was only used with bank 128 (for percussion), and bits 2–8 were used to select a single bank between 0 and 127. Bits 9–16 were unused.

Starting from SFe draft specification milestone 4.0.9b, `wBank` is replaced with `byBankMSB` and `byBankLSB`.
- This change is completely backwards compatible as there is no change in the format. It is simply for specification readability reasons.
- RIFF formats (with the exception of RIFX) are little endian. Therefore, `byBankMSB` goes before `byBankLSB`.
- Like with `wBank` in SF2.04, bits 2–8 are now used to set the first bank change.
- If a bank/program change combination produces a different result for midi channel 10, use the percussion toggle in `byBankMSB`.
- File editors should warn the user if this issue is found.
- SFe compatible players should allow the user to swap CC00 and CC32 settings.
- Order in the `phdr` chunk in terms of ascending `byBankLSB` value to ensure legacy SF compatibility.

### Definitions of `dwLibrary` and `dwGenre`

Old 2.04 fields `dwLibrary` and `dwGenre` are now defined.

- `dwLibrary` is for the overall name of the set of files contained in a library of SFe 4 files.
    - This value will correspond to a list in an enum. This is planned for 4.4.
- `dwGenre` is for the genre of music which the files are optimized for.
    - This value will correspond to a list in an enum. This is planned for 4.4.
- `dwMorphology` has been left out of this draft specification. It will eventually be re-introduced in a future version.

### Do not access the final `sfPresetHeader` entry

The last sfPresetHeader entry shouldn't need to be accessed, apart from the uses described in `SFSPEC24.PDF`.

### This is a required sub-chunk

Files without a `phdr` sub-chunk are "Structurally Unsound."

* * *

## 7.3 `pbag` sub-chunk

This refers to the "Preset Bag" of the SFe file. This sub-chunk is a multiple of 4 bytes.

Its structure is the same as in legacy SF2.04.

All values in this sub-chunk should be used as directed in `SFSPEC24.PDF`.

### This is a required sub-chunk

Files without a `pbag` sub-chunk are "Structurally Unsound."

* * *

## 7.4 `pmod` sub-chunk

The `pmod` sub-chunk is a multiple of 10 bytes.

The structure is identical to legacy SF2.04's `pmod` structure for SFe 4.0. SFe 4.1 will add new features.

Legacy SF players which do not support any new enum options in SFe 4.1 or later should ignore these new options.

This enum, and all other enums, is two bytes in length.

### This is a required sub-chunk

Files without a `pmod` sub-chunk are "Structurally Unsound."

* * *

## 7.5 `pgen` sub-chunk

The `pgen` sub-chunk is a multiple of four bytes, like in legacy SF2.04.

The structure and type definitions are the same as in legacy SF2.04. SFe 4.1 will add new features. Legacy SF players which do not support any new enum options in SFe 4.1 or later should ignore these new options.

This enum is two bytes in length.

### This is a required sub-chunk

Files without a `pgen` sub-chunk are "Structurally Unsound."

* * *

## 7.6 `inst` sub-chunk

The inst sub-chunk is a multiple of 22 bytes.

### achInstName Changes

- In legacy SF2.04, `achInstName` must be an ASCII string.
- Now, UTF-8 replaces ASCII, allowing more characters to be written.

### This is a required sub-chunk

Files without an `inst` sub-chunk are "Structurally Unsound."

* * *

## 7.7 `ibag` sub-chunk

This refers to the "Instrument Bag" of the SFe file.

This sub-chunk is a multiple of four bytes. This is like the `pbag` sub-chunk.

All values in this sub-chunk should be used as directed in `SFSPEC24.PDF`.

### This is a required sub-chunk

Files without an `ibag` sub-chunk are "Structurally Unsound."

* * *

## 7.8 `imod` sub-chunk

The `imod` sub-chunk is a multiple of 10 bytes, like the `pmod` sub-chunk.

The structure is very similar to legacy SF2.04's `imod` structure, with these differences:

### New options for the `SFModulator` enum

These options are listed elsewhere in the specification. Currently, SFe 4.0 does not define any new options.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum, and all other enums, is two bytes in length.

### Preset and instrument modulators

The Preset Modulator values are added to the Instrument Modulator values, and that is the final modulator used.

### This is a required sub-chunk

Files without an `imod` sub-chunk are "Structurally Unsound."

* * *

## 7.9 `igen` sub-chunk

The `igen` sub-chunk is a multiple of four bytes, like the `pgen` sub-chunk.

### New options for the `SFGenerator` enum

These options are listed elsewhere in the specification. Currently, SFe 4.0 does not define any new options.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum is two bytes in length.

### This is a required sub-chunk

files without an `igen` sub-chunk are "Structurally Unsound."

* * *

## 7.10 `shdr` sub-chunk

The `shdr` sub-chunk contains the headers for the sample data.

It is a multiple of 46 bytes.

### `achSampleName` Changes

- In legacy SF2.04, `achSampleName` must be an ASCII string.
- Now, UTF-8 replaces ASCII, allowing more characters to be written.

### Sample Rate Limit Changes

- In SFe, sample rates (`dwSampleRate`) are stored as a 32-bit integer. This is the same behavior as seen in the legacy SF2.04 format. This results in a theoretical maximum sample rate of 4,294,967,295 Hz.
- In the legacy SF2.04 specification, E-mu suggested that sample rates of below 400 Hz or above 50,000 Hz should be avoided as some legacy hardware platforms may not be able to reproduce these sounds. This is not a limitation of the specification, but rather a limitation of legacy sound cards.
- Despite this, Creative did not use 16-bit integers for sample rate in legacy SF2.04. It is thus safe to use sample rates in excess of 50,000 Hz. If a sample rate of below 400 Hz or above 50,000 Hz is encountered, no attempt should be made to change the sample rate.
- A zero sample rate should be reset.

### `sfSampleType` and SFe Compression

Bit 4 of `sfSampleType` is reserved for SFe Compression usage.

- Read the SFe Compression specification!

The `sfSampleType` enum is two bytes in length.

### This is a required sub-chunk

Files without a `shdr` sub-chunk are "Structurally Unsound."

# Section 8: Enumerators

## 8.1.1 Kinds of generator enums

These are identical to legacy SF2.04.

* * *

## 8.1.2/3 Generator enums definitions

The Generator Enums used in SFe 4.0, are the same as the legacy SF2.04 standard. SFe 4.1 will include an overhaul of the modulator system, including new enums.

* * *

## 8.2.1 Source enum controller palettes

These are identical to legacy SF2.04.

* * *

## 8.2.2-3 Source Directions and Polarities

These are identical to legacy SF2.04.

* * *

## 8.2.4 Source Types

In legacy SF2.04, there are four sources.

* * *

## 8.3 Modulator transform enums

These are identical to legacy SF2.04 in SFe 4.0, but SFe 4.1 will include an overhaul of the modulator system, including new enums.

* * *

## 8.4.1-4 Default modulators 1-4

These have been removed, and no longer exist in SFe 4.0, but the default modulator definition will be allowed in SFe 4.1.

* * *

## 8.4.5-10 Default modulators 5-10

These are identical to legacy SF2.04.

* * *

## 8.5 Precedence, Absolute/Relative Values and Preset Level Availability of Generators.

The rules for precedence and absolute/relative values are identical to legacy SF2.04.

# Section 9: Parameters and synthesis model

## 9.1 SFe 4 synthesis model

In SFe, the synthesis model will have massive improvements compared to the EMU8000-based synthesis model of legacy SF2.04 and Werner SF3 over time. Currently, it is identical to the synthesis model of legacy SF2.04, but 4.1 will add the first improvements.

A version of SFe in the far future will have a programmable synthesis model. 

* * *

## 9.1.1 Sample-based oscillator

The method of operation is identical to legacy SF2.04.

* * *

## 9.1.2 Sample looping

The method of operation is identical to legacy SF2.04, but different types of looping will be added in SFe 4.2.

* * *

## 9.1.3 Filters

The method of operation is identical to legacy SF2.04, but different types of filters will be added in SFe 4.1.

* * *

## 9.1.4 Final gain amplifier

The method of operation is identical to legacy SF2.04.

* * *

## 9.1.5 Effects Sends

The method of operation is identical to legacy SF2.04, but the chorus and reverb effects will be replaceable with different versions starting with SFe 4.1.

* * *

## 9.1.6 Low Frequency Oscillators (LFOs)

There are two LFOs, which work in the same way as legacy SF2.04.

* * *

## 9.1.7 Envelope Generators

There are two envelope generators which work in the same way as legacy SF2.04.

* * *

## 9.1.8 Modulation interconnection

\[Insert figures of modulation interconnection\]

* * *

## 9.2 MIDI functions

Control Change #32 (Bank Select "LSB") has been modified to use the `byBankLSB` value.

All other MIDI functions are unchanged from legacy SF2.04.

If a SoundFont® 2.00a file is loaded, see `SFSPEC24.PDF` for more details for handling of SoundFont® 2.00 files.

* * *

## 9.3 Parameter units

All of these are the same as legacy SF2.04.

* * *

## 9.4 SF Generator Model

This is the same as legacy SF2.04.

* * *

## 9.5 SF Modulator Model

- Modulators work in the same way as legacy SF2.04, but an update will be made in SFe 4.1.
- \[New diagrams available soon\]

* * *

## 9.6 NRPN implementation

The NRPN implementation used by SFe 4.0 is identical to legacy SF2.04.

* * *

## 9.7 On implementation accuracy

E-mu was very lax when it came to accuracy of legacy SF implementations. This was because of the limitations of computers and legacy soundcards that the legacy SF spec and its implementations were initially designed to run on. While this was the only way that legacy SF could gain the popularity that it did with software implementations, this meant that bank developers often had to declare the program that their file was intended to be used with. This hampered interoperability with different SF players, including those that may have been embedded into musical instruments.

Because today's computers are much faster, and legacy soundcards are no longer in widespread use, the requirements for implementation accuracy in SFe are far more strict. All SFe players are required to recognise the `flag` sub-chunk (section 5.12.2) and warn the user if there is a mismatch between feature flags in the bank and the program's support.

While the `flag` sub-chunk will be useful to alert users about incompatible programs, program developers should make an effort to ensure that their program is 100% compatible.

# Section 10: Error-handling

## 10.1 Structural errors

The error correction process for structural errors in SFe is slightly different from that in legacy SF2.04:

- If a `ds64` chunk, `BW64` or `RF64` header is found in a file, SFe players that do not support 64-bit chunk headers should output a specific error, as mentioned in the SFe program specification.
- If the `ds64` chunk is missing, the bank uses a 32-bit chunk header. Make sure that `ckSize` is accurate, using the same techniques as for SF2.04.
    - If the value of `ckSize` is 4,294,967,295 (like in `ds64`), or any other inaccurate value, reject the file as "Structurally Unsound."
    - If the value of `ckSize` is correct, open the file and output a warning message, as mentioned in the SFe program specification.
    - More advanced programs may also recognize files larger than 4GiB with 32-bit headers. However, such a file should be repaired with a 64-bit header as soon as possible.
- Banks with 64-bit headers, but with a `ckSize` value that is not 4,294,967,295 should be rejected as "Structurally Unsound," as this is not valid in RIFF64.

* * *

## 10.1a Duplicated preset locations within files

This occurs when the file is structurally damaged or manually edited in a manner where more than one preset has the same value of byBankMSB, byBankLSB and wPreset (for instance, 015:000:081).

- In legacy SF2.04, the first preset in the location would be used by default, but the other presets would still be retained.
- Such other presets must be moved before they can be used.
- In SFe, the preset to be used is no longer necessarily the first one. Instead, selecting the correct preset (or combination of presets) to use will be permissible.
- Such a feature is optional, and if not implemented, the player should use the legacy SF2.04 behavior in these cases (use the first preset found).
- Editors should warn the user if such presets are found.
- This behavior might change in future versions, so please take the `ifil` value, and later versions of this specification, into account. In particular, later versions of SFe will use the `ISFe-list` sub-chunk to determine this behavior.

* * *

## 10.1b Duplicated preset locations across files

This occurs when multiple files are loaded simultaneously (now a required feature for SFe), but some or all of the files have presets with identical `byBankMSB`, `byBankLSB` and `wPreset` values.

- Behavior was undefined in legacy SF2.04.
- This was because multiple file loading was not a standard feature mandated in the legacy SoundFont® standard.
- Legacy SF2.04 and Werner SF3 compatible software developers therefore had the liberty to implement multiple file loading; however, they wanted to.
- This edge case will now be defined in SFe.
- If multiple presets across loaded files have the same value of `byBankMSB`, `byBankLSB` and `wPreset`, then the preset to be used may be selectable from all the presets with the same bank location, depending on the player implementation. The preset to be used may also be a combination of multiple presets.
- Such a feature is also optional, and if not implemented, you can either use the first preset found, or you can combine all the presets.
- This behavior might change in future versions, so please take the `ifil` value, and later versions of this specification, into account. In particular, later versions of SFe will use the `ISFe-list` sub-chunk to determine this behavior.

* * *

## 10.2 Undefined chunks

legacy SF2.04 players should ignore SFe-specific sub-chunks, as prescribed by E-mu.

Also, SFe 4.0 compatible players, which do not support future versions, should ignore sub-chunks which are used in future versions.

* * *

## 10.3 Unknown Enumerators

Any ifil versions of 4.1 or above may have unknown enumeration values for an SFe 4.0 player.

This is entirely expected, and if unknown enumeration values are found, the Generator/Modulator should be ignored.

* * *

## 10.4 Illegal Parameter Values

Illegal parameter values are handled as in legacy SF2.04.

* * *

## 10.5 Out of Range Values

Out of range values are handled as in legacy SF2.04.

* * *

## 10.5a Exceeded Maximum File Size Limit

This occurs when the user loads a file that is larger than the maximum size that the SFe program can accommodate.

- In the AWE32 and AWE64, the limit was dependent on the memory installed on the card, which was up to 28 MiB.
- Later, the sound cards allowed the user to load files with file sizes up to system memory.
- SFe has defined limits that are found in the separate program specification.
- If these limits are reached, you can reject loading of the file with an error, or attempt to load the file anyway.
- SFe programs should warn the user if processing was automatically done to a file to reduce the file size to be in range.
- If multiple files are loaded, and the limit is reached, the order of files to be loaded can be defined by the author of the SFe-compatible software.

* * *

## 10.6 Missing Required Items

If required items are missing, it is handled as in legacy SF2.04.

* * *

## 10.7 Illegal Enumerators

Illegal enumerators are handled as in legacy SF2.04.

# Section 11: SiliconSFe

Traditional SiliconSF banks are provided for compatibility purposes only, but we are unaware of any shipping products using SiliconSF.

Except for when size concerns prohibit its inclusion, SFe players should include an AWE ROM emulator.

- The AWE ROM emulator includes 152 samples.
- The file size should be 1MB, as all samples should be to the same standard as the original.
- Samples which the program developer has the right to use can be used as a replacement for the original ROM samples.
- Freely-usable reference implementation samples are available, but are not intended for production use.
- Sample names will remain the same, but there will be acceptable alias names.
- Emulators should also be able to open up SF files (either legacy SF or SFe) containing samples and metadata.
- There may or may not be instruments or presets.

The new system will also permit real time synthesis.

- Basic waveforms are provided.
- They should be generated in real time, not from samples.
- Wavetable synthesis can also be combined with different sounds.

Read the legacy SF2.04 specification for information on how to make custom Silicon SF banks for older hardware.

A SiliconSFe specification will be available in the final specification.

# Section 12: Glossary

This glossary is broadly the same as the glossary in `SFSPEC24.PDF`, with these additions and changes:

- Articulation - Modulation of available parameters and usage of extra samples to produce expressive musical notes.
- AWE64 - The successor to the famous AWE32, adding features such as waveguide synthesis. Used the EMU8000 synthesizer chip, like the preceding AWE32. Available in "Value" or "Gold" versions.
- Branch - A subdivision of a tree strucutre containing either sub-branches or leaves that include values.
- BW64 - Broadcast Wave 64, used in the RF64 Header.
- Case-insensitive - Indicates that a UTF-8 character or string treats alphabetic characters of upper or lower case as identical.
- Case-sensitive - Indicates that a UTF-8 character or string treats alphabetic characters of upper or lower case as distinct.
- Cognitone SF4 - An incompatible modification to Werner SF3 to allow support for FLAC audio compression. Because it is considered proprietary compression, usage is not allowed in SFe.
- DAHDSR - Stands for Delay, attack, hold, decay, sustain, release. The six-step envelope system used in SF and SFe. 
- Downloadable - legacy SF2.0x, Werner SF3 or SFe file obtained from the internet. (Old meaning referred to the obsolete ROM system)
- Dynamic RIFF - A RIFF-type format by spessasus to allow formats to scale beyond 64-bit, while saving space. Implemented in future SFe versions. 
- EMU10K1 - The successor to the EMU8000, designed by E-mu® for the Creative Labs SB Live!.
- EMU10K2 - An update to the EMU10K1, designed by E-mu® for the Creative Labs SB Audigy.
- EMU20K1 - The successor to the EMU10K2, designed by E-mu® for the Creative Labs SB X-Fi.
- EMU20K2 - An update to the EMU20K1, please refer [here](https://en.wikipedia.org/wiki/Sound_Blaster_X-Fi) for information on SB X-Fi cards that include it.
- FLAC - A lossless audio compression format commonly used in open-source software. Supported by Werner SF3, but not commonly used for that purpose.
- Hold - The portion of the DAHDSR envelope after the attack portion, but before the decay portion starts.
- Leaf - A value found in a tree structure at the end of a branch.
- Legacy sound card - A Sound Blaster® (or other sound card) that uses a hardware MIDI synthesiser capable of using banks in the SoundFont® format.
- Lossless compression - Said of a compression format that retains all of its data when compressed. In terms of audio, there is no loss in quality in losslessly compressed audio.
- Lossy compression - Said of a compression format that does not retain all of its data when compressed. In terms of audio, there is a loss in quality in lossily compressed audio.
- MIDI Bank - Groups of up to 128 presets, which can be selected by the two MIDI "Bank Select" control changes (CC00 and CC32).
- OGG - See "Vorbis".
- Opus - A lossy audio compression format, slightly newer than OGG but with less wide adoption.
- Proprietary Compression - Any non-Werner SF3 SoundFont® compression system. Usage is not allowed in SFe.
- RF64 - See "RIFF64".
- RIFD - See "Dynamic RIFF".
- RIFF64 - A 64-bit RIFF-type format. Contrast to the RIFF format, which is 32-bit. Therefore, the maximum file size is above 4 gigabytes in size.
- RIFF-type format - Formats similar to RIFF (Resource Interchange File Format), see "RIFF" in `SFSPEC24.PDF` for more information.
- ROM samples - Obsolete feature used in legacy sound cards, most modern SF2 files do not use this feature.
- SB - Abbreviation of "Sound Blaster®". For example, "SB X-Fi".
- SFe - A family of enhancements to the SoundFont® 2.04 formats, unofficially created after E-mu/Creative abandoned the original format. May not be structurally compatible with legacy SF2.04.
- SFe 4 - This new specification, based on SoundFont® 2.04 and Werner SF3, with a set of new features making it more realistic. Not to be confused with the incompatible Cognitone SF4 file format.
- SFe-compatible - Indicates files, data, synthesisers, hardware or software that conform to the SFe specification.
- SFe Compression - The compression system based on Werner SF3 that SFe programs should be compliant with.
- Sound Blaster® Live! - The successor to the AWE64, which improved the synthesizer chip to the EMU10K1, supporting modulators.
- Sound Blaster® Audigy - The successor to the SB Live!, containing the EMU10K2 chip.
- Sound Blaster® X-Fi - The successor to the SB Audigy, containing the EMU20K1 or EMU20K2 chip. Supports 24-Bit SoundFont® 2 files (2.04).
- Static RIFF - Any RIFF-type format with a fixed chunk size field width, including RIFF or RIFF64. See "RIFF-type format", "RIFF" and "RIFF64".
- Synth - Abbreviation of "Synthesiser," see "Synthesiser" in `SFSPEC24.PDF` for more information.
- Tree structure - A structure consisting of branches and leaves.
- Version 3 - See "Werner SF3".
- Version 4 - See "SFe 4".
- Vorbis - A lossy audio compression format commonly used in open-source software. The basic compression format that most Werner SF3 and SFe-compatible software should be expected to implement.
- Werner SF3 - A small upgrade to SoundFont® 2.04 created by Werner Schweer to allow an open source compression solution for SoundFont® programs. Standardised as SFe Compression.