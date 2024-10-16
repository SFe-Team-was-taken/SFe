# SF-enhanced 32-bit (SFe32) specification

## Version 4.00.7c (draft specification) - Revision C

Copyright 2020-2024 SFe Team

Based on the abandoned E-mu spec, which is copyright 1994–2002 E-mu Systems Inc.

* * *

## 0.1 Revision history

|               |                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Revision      | Date                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 4.00.7c       | October 17, 2024     | First 32-bit specification with structural changes from SFe64. <br> Fixed some more things <br> Name update                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 4.00.7b       | October 12, 2024     | Updated program SFe32-to-SFe64 specification <br> Fix capitalisation in 1.5a <br> Remove extraneous table of contents entries <br> Fix more registered trademark symbols <br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 4.00.7a       | October 10, 2024     | Table of contents added <br> Merge the pages into one <br> Fix the typos and formatting <br> Special thanks for spessasus for authoring these changes! <br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 4.00.6        | October 3, 2024      | Added milestone classification for some draft specifications in 0.1a  <br>Removed all SFe32-specific information, renamed to SFe64 spec  <br>Renamed 3.1a to 3.1, 6.1a to 6.1, 6.1b to 6.1a, 6.2a to 6.2, and 6.2b to 6.2a, for consistency  <br>Delayed modulator update to version 4.01  <br>Removed 7.1a, because it's not relevant to versions before 5.00  <br>Added LSB to example value in 10.1a  <br>Added more information about future plans  <br>Reworked SFe64 to be a simple 64-bit extension to SFe32 for now, features will come later                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 4.00.5c       | September 2, 2024    | Added clarification for timeframe in which 0.4 will be filled out  <br>Rewritten 1.1a to be clearer, moving links from 1.1b  <br>Removed redundant "important" words in 1.1b  <br>Moved some compatibility info from sections 1.3 and 3.1 to compatibility spec  <br>ROM samples no longer listed as deprecated in 3.2, 5.4, 5.5 and 6.1a  <br>Error handling plans for version 4.00.6 added in 3.3  <br>Fixed capitalisation in 4.5  <br>Added section 4.5a for file format extensions, removed .sf32 and .sf64  <br>Removed isfe reference for 5.1, SFe32 programs can determine WernerSF3 with wMajor=3  <br>Fixed reference to compatibility spec in 5.1a, compatibility spec is not used in SFe64  <br>Rewritten 5.2 to make it clearer, and to mention default modulator definitions for 4.01.  <br>Added heading 3 in formatting of section 7 and section 7.1a for subchunk size alignment.  <br>Removed reverb/chorus definitions in 8.1.2, 8.1.3 and 9.1.5 (will be restored in 4.01)  <br>Fixed some other typos and added a few other clarifications                                                                                                         |
| 4.00.5b       | September 1, 2024    | Clarified information about sample rates in section 7.10                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 4.00.5a       | August 30, 2024      | All remaining SF32/SF64 references should now be renamed to SFe32/SFe64  <br>Added ROM sample specification for the AWE ROM emulator  <br>Replaced draft number references with the new versioning system  <br>Added clarification for the compatibility specification versioning  <br>Fixed mistake in INFO chunk information in the compatibility specification  <br>Clarified that this document is not created by E-mu  <br>Added placeholder for the SF Server link  <br>Specific version number added to title  <br>Added instructions to compatibility spec about how to handle incompatible compression  <br>Error messages modified to remove scom reference and fix version 3 reference to version 4  <br>Added section 1.5a to mention future plans for the SFe format  <br>Added 0.1a to describe specification versioning  <br>Removed unnecessary information about Creative Technology  <br>Proprietary compression formats are now forbidden in the program specification  <br>Added references to SFe Team; a list of developers can be found in 0.3a.  <br>Next version for release by early 2025 will have the SFe file repair program specification |
| 4.00.4        | July 4, 2024         | Clarified about legacy compliance and TSC in section 3.2.  <br>Added more clarification in revision history  <br>8-bit mode information updated again  <br>Added info about how SFe32 can be parsed as SFe64  <br>More information about the pdta structure added  <br>Real time synthesis is no longer mandatory  <br>Renamed to version 4 and updated versioning scheme  <br>Added preliminary Werner SF3 compatibility  <br>Removed scom sub-chunk  <br>For now, removed increased character limits in SFe32.  <br>Changed sleaf's name on the contact.  <br>Added information on bank select and TSC mode  <br>Added the isfe sub-chunk for SFe64  <br>One mention of "back and forth" now "bidirectional"  <br>Added and clarified some terms in glossary  <br>Stated that incompatible compression is no longer allowed in 6.1b.  <br>Renamed SF32 and SF64 to SFe32 and SFe64.  <br>Added clarification of "SFe format developers" in 1.5.  <br>Moved compatibility information to the compatibility specification.  <br>Added 5.1a to describe ifil sub-chunk versioning.                                                                                       |
| 4.00.3        | September 6, 2022    | Added clarification  <br>Renamed 32-bit SF version 3 to SF32  <br>Overall format has been renamed to SFe (SF enhanced)  <br>wBank bit 9 is no longer reserved.  <br>Silicon SF banks for SF64  <br>Added CM reset  <br>Changed isng value  <br>Fixed some pdta sub-chunks for SF64  <br>Corrected sfSampleType reference from bit 15 to bit 16.  <br>Renamed "back and forth" to "bidirectional"  <br>Changed "improved" to "fixed" in revision log  <br>Added a nicer diagram (can you find it?)  <br>Fixed extraneous reference to wBank2 in section 4.  <br>Modified information about the scom sub-chunk.  <br>8-bit mode information updated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 4.00.2        | July 22, 2022        | Renamed 64-bit SF3 to SF64 version 3  <br>32-bit SF3 is now 32-bit SF version 3  <br>Changed ASCII to UTF-8  <br>Fixed the wPreset and wBank (removed wBank2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 4.00.1        | April 12, 2020       | First version                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| (2.04)        | (September 10, 2002) | (Last version authored by E-mu until format abandoned)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

* * *

## 0.1a Specification Versioning

Final specifications have version numbers in the format x.yyL, where x and y are numbers and l is a letter:

- x is incremented when a change in the SFe64 format is made in a way that makes the resulting files incompatible with the previous version.
- y is incremented when there are new features added to either the SFe64 or the SFe32 format.
- SFe32 may skip "y" versions, because there will be SFe64-only feature additions in the future.
- L is incremented when there are small changes made to the specification, if L is absent, then assume that it is "a."
- An example of a final specification version would be 4.00.

Draft specification milestones have version numbers in the format x.yy.zL, where x, y and z are numbers and L is a letter. In this case, the versioning works similarly to a final specification, but with these changes:

- z is incremented when the draft undergoes a larger change, or large updates are made to the software.
- L is incremented when there are small changes, but only when pointed out by others.
- An example of a draft specification version would be 4.00.5.

During the development of specifications, version numbers will be in the format x.yy.aaaabbccL, where x, y, z, a, b and c are numbers, and L is a letter. The versioning is similar to final specifications and milestone drafts, but aaaabbcc is the day in which the specification was updated, and L is incremented when updated.

The revision history table refers to development versions as "This version" and includes the cumulative changes made to the specification since the last milestone revision.

* * *

## 0.2 Disclaimers

We don't own the rights to use the term "Soundfont," so the term SF is used instead.

The trademark rights to the term "Soundfont" belong to Creative Technology Ltd.

That being said, "soundfont" is rapidly becoming a genericised word via the actions of the VGM (video game music) and lightsaber communities (despite the lightsaber community not using .sf2 files, and misusing the term for another format).

We urge rights holders (Creative Technology Ltd.) to prevent the lightsaber community from appropriating the trademark for their unrelated format.

All excerpts from the SF 2.04 specification are copyrighted by E-mu Systems or Creative Technology Ltd, and are only used for reference. Everything should fall under fair use rights.

We are confident that the base file format is not copyrightable, but we are able to take this document down if necessary.

This is a draft. Expect errors, and feel free to report them. Sylvia-leaf has access to a computer with a Sound Blaster X-Fi Titanium, so she will be able to test or reproduce any issues found on real hardware.

Do not use "draft" specifications (version number x.yy.zL) to base final products on. Always refer to a "final" specification (version number x.yyL).

* * *

## 0.3 Updates and comments

The website "soundfont.com" is dead (last archive.org snapshot we could found was 2012/13), and the provided email on the SF 2.04 spec probably doesn't work, so contact the SFe Team:

- GitHub: https://github.com/SFe-Team-was-taken

A link to the SF Server Discord will be provided soon.

* * *

## 0.3a SFe Team

SFe Team members:

- sylvia-leaf (she/her) | Discord - @tanukilvia | Email - sylvialeaf6284@gmail.com
- Stgiga (they/them) | Discord - @stgiga

Special thanks to these people for contributions: spessasus
Thanks to these people for suggestions: derselbst, mawe42, Saga

Want to join the SFe Team? Please contact sylvia-leaf using the contacts in section 0.3.

* * *

## 0.4 Table of contents

<!-- Table of contents: contributed by @spessasus. -->
* [SF-enhanced 32-bit (SFe32) specification](#sf-enhanced-32-bit-sfe32-specification)
  * [0.1 Revision history](#01-revision-history)
  * [0.1a Specification Versioning](#01a-specification-versioning)
  * [0.2 Disclaimers](#02-disclaimers)
  * [0.3 Updates and comments](#03-updates-and-comments)
  * [0.3a SFe Team](#03a-sfe-team)
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
* [Section 2: Terms and abbreviations](#section-2-terms-and-abbreviations)
  * [2.1 Data structure terminology](#21-data-structure-terminology)
  * [2.2 Synthesis terminology](#22-synthesis-terminology)
  * [2.3 Parameter terminology](#23-parameter-terminology)
* [Section 3: RIFF and RF64 structure](#section-3-riff-and-rf64-structure)
  * [3.1 General RIFF and RF64 file structures](#31-general-riff-and-rf64-file-structures)
  * [3.2 Chunks and subchunks in version 4](#32-chunks-and-subchunks-in-version-4)
  * [3.3 Error handling](#33-error-handling)
* [Section 4: RF64 file format of SFe32, version 4.00](#section-4-rf64-file-format-of-sfe32-version-400)
  * [4.1-4.4 File structure of version 4](#41-44-file-structure-of-version-4)
  * [4.5 Type definitions](#45-type-definitions)
  * [4.5a File format extensions](#45a-file-format-extensions)
* [Section 5: "info-list" chunk](#section-5-info-list-chunk)
  * [5.1 "ifil" subchunk](#51-ifil-subchunk)
  * [5.1a Versioning rules](#51a-versioning-rules)
  * [5.2 "isng" subchunk](#52-isng-subchunk)
  * [5.3 "INAM" subchunk](#53-inam-subchunk)
  * [5.4 "irom" subchunk](#54-irom-subchunk)
  * [5.5 "iver" subchunk](#55-iver-subchunk)
  * [5.6 "ICRD" subchunk](#56-icrd-subchunk)
  * [5.7 "IENG" subchunk](#57-ieng-subchunk)
  * [5.8 "IPRD" subchunk](#58-iprd-subchunk)
  * [5.9 "ICOP" subchunk](#59-icop-subchunk)
  * [5.10 "ICMT" subchunk](#510-icmt-subchunk)
  * [5.11 "ISFT" subchunk](#511-isft-subchunk)
  * [5.12 "ISFe" subchunk](#512-isfe-subchunk)
* [Section 6: "sdta-list" chunk](#section-6-sdta-list-chunk)
  * [6.1a "smpl" sub-chunk](#61a-smpl-sub-chunk)
  * [6.1b About compression in SFe32](#61b-about-compression-in-sfe32)
  * [6.2a "sm24" and "sm32" sub-chunk](#62a-sm24-and-sm32-sub-chunk)
  * [6.2b Using 8-bit samples](#62b-using-8-bit-samples)
  * [6.3 Looping rules](#63-looping-rules)
* [Section 7: "pdta-list" chunk](#section-7-pdta-list-chunk)
  * [7.1 "Hydra" structure](#71-hydra-structure)
  * [7.2 "phdr" sub-chunk](#72-phdr-sub-chunk)
    * [wPreset Changes](#wpreset-changes)
    * [wBank Changes](#wbank-changes)
    * [Definitions of dwLibrary and dwGenre](#definitions-of-dwlibrary-and-dwgenre)
    * [Do not access the final sfPresetHeader entry](#do-not-access-the-final-sfpresetheader-entry)
  * [7.3 "pbag" sub-chunk](#73-pbag-sub-chunk)
  * [7.4 "pmod" sub-chunk](#74-pmod-sub-chunk)
    * [New options for the SFModulator enum](#new-options-for-the-sfmodulator-enum)
  * [7.5 "pgen" sub-chunk](#75-pgen-sub-chunk)
    * [New options for the SFGenerator enum](#new-options-for-the-sfgenerator-enum)
  * [7.6 "inst" sub-chunk](#76-inst-sub-chunk)
  * [7.7 "ibag" sub-chunk](#77-ibag-sub-chunk)
  * [7.8 "imod" sub-chunk](#78-imod-sub-chunk)
    * [New options for the SFModulator enum](#new-options-for-the-sfmodulator-enum-1)
    * [Preset and instrument modulators](#preset-and-instrument-modulators)
  * [7.9 "igen" sub-chunk](#79-igen-sub-chunk)
    * [New options for the SFGenerator enum](#new-options-for-the-sfgenerator-enum-1)
  * [7.10 "shdr" sub-chunk](#710-shdr-sub-chunk)
    * [Sample Rate Limit Changes](#sample-rate-limit-changes)
    * [sfSampleType and Werner SF3](#sfsampletype-and-werner-sf3)
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
  * [9.1 SFe version 4 synthesis model](#91-sfe-version-4-synthesis-model)
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

- This is a draft specification for the SFe32 file format, version 4.00, based on the famous E-mu Systems® SoundFont® 2.04, and Werner SF3 standards.
- It's intended to be a source of information on SFe32.
- To create files that support SFe32, you will need:
    - The SFe32 format, compatibility, and program specifications
    - E-mu's provided documents for SF 2.04 ([sfspec24.pdf](https://freepats.zenvoid.org/sf2/sfspec24.pdf))
    - The Werner SF3 specification ([draft by FluidSynth](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format))
- All features from version 2.04 will be retained.

* * *

## 1.1b Important differences from the 2.04 document

- This is not a standalone document; it refers to both the SF 2.04 and Werner SF3 technical specifications.
- This document is unofficial and was not created by E-mu. If you want this to be removed, we will remove it, but we hope that this is because you have your own update to the SF format ready.
- For copyright reasons, we cannot copy information from the original standard, except for what is required to interpret this document and what is allowed under fair use.

* * *

## 1.2 Document organisation

The sections in this specification map to the E-mu Systems® SoundFont® 2.04 specification document.

- Like the version 2.04 specification, section 1 and 2 gives introductory information about SFe32.
- Sections 3–8 provide detailed information about the updates made to the SFe32 structure.
- Section 9 shows the synthesis engine.
- Section 10 describes any error handling that is necessary when opening SFe32 files.
- Section 11 describes legacy ROM methods of storing an SFe32 file.
- Section 12 is a glossary of most terms in this draft specification.

New sections may be added in the future, depending on if radical changes are made to the format.

* * *

## 1.3 SFe objectives

### The SFe32 standard has been created to provide a 64-bit successor to E-mu Systems®'s SoundFont® 2.04 standard, with many different new features which are required to increase realism of virtual instrument banks further.

- the file size limit remains 4GiB, and the data types remain the same.
- there will be a few new modulators in the future
- the feature set will be a subset of the more advanced SFe64 format, including the critical features that are not found in the current versions 2 and 3 format to bring the popular install base of the SF2/SF3 format forward to the 21st century and beyond; it will also act as a stepping stone between SF2/SF3 and SFe64, which is our vision of the monolithic sample library of the future.
- ROM features for legacy sound cards will also be kept, to allow the ROM samples inside these old sound cards to be used with the new features.
- compatibility with legacy SF players that fully implement the legacy SF specification will continue; all that is needed is usage of the sf2 extension, and it should be possible to load an SFe32 file, on existing software.
- a version will not release if the resulting features break the forward compatibility of legacy soundfont players; we will test updates before releasing final versions.
- compatible players will require a certain standard of features, which is in the separate SFe32 program specification.


* * *

## 1.4 The background of the SF format

SoundFont® 1 refers to the proprietary version of the format used by the Creative Sound Blaster® AWE32 sound card released in 1994.

- SoundFont® one files had a file extension of .SBK and cannot be used by many of SF 2.0x programs.
- This is the version used in the Creative DOS drivers.
- Creative is the brand name used by the company "Creative Technology Ltd."
- As the specification for SF 1 was never released, we don't know how SF 1 files were structured.

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

Current Creative Labs sound cards do not support the SoundFont® format; the Audigy RX from 2013 was the last model that supported the format. Newer cards, for instance, the AE-9, no longer use wavetable sound synthesis.

At an unknown time, Kenneth Rundt, the author of SynthFont and a series of products based on it, added some custom features, mostly ported over from the DLS format:

- Always play the sample to the end
- Velocity to volume envelope attack (from DLS)
- Velocity to modulation envelope attack (from DLS)
- Vibrato lfo to volume (from DLS)

Werner Schweer found a way to compress SoundFont® 2 files (with the lossy Vorbis format).

- The resulting format was known as SF3.
- It is commonly used by open source programs.
- This is the reason why this format is not called .SF3 (it was in 4.00.1, but after **feedback by derselbst** and **mawe42** on GitHub, we changed it to SFe32 and SFe64).
- SFe files will be compatible with Werner SF3 for compression.

Another development was done by Cognitone, which created an open source program that can losslessly compress SoundFont® 2 files (with FLAC).

- This was unofficially called SF4.
- This is intended to be the true version 4, as Cognitone SF4 seems to not have been as widespread as SF3.
- SF4 has also been rejected by the Werner SF3 community as too loosely defined.

Finally, stgiga found out that many programs don't mind RIFF64 (RF64) files. This is the purpose of the SFe64 format and thus beyond the scope of SFe32.

This is where we stand right now.

* * *

## 1.5 Improvements and enhancements

SFe32 (version 4) is designed for future improvements.

- These will be done in a more liberal way than the conservative manner of the SoundFont® 2 updates that E-mu® has done.
- SFe32 will have a reduced set of improvements, as it is designed to be completely backward compatible with SF2.04.
- No version of SFe32 will become incompatible with fully compliant SF2.04 software.
- Eventually, we will permanently freeze SFe32, only if and when SFe64-compatible software has reached significant acceptance.
- After the feature freeze, SFe32 will remain a dependable and stable format for software development to be based on.
- To avoid over-stress of developers of the SFe Team, as well as SFe instrument banks, features will be spread out across versions. We hope to release a new version every 3-5 years.
- SFe32 development can be done in tandem with SFe64.

* * *

## 1.5a Plans

The features for version 4.00 have been frozen after the release of version 4.00.4. This doesn't mean that we're done with SFe, in fact, this is only the beginning of the format's development.

We decided to do a feature freeze for version 4.00 to make sure that SFe program developers have a reasonable set of features to implement. If we add too many features, it can overwhelm developers.

Here are a few things that are planned for SFe:

- For SFe32 draft specification milestone 4.00.8, we are planning to introduce the SFe file repair program specification. This was intended for 4.00.7, but we have merged a pull request from spessasus that fundamentally changes the structure of the specification (merges all sections into one file), so it could not remain version 4.00.6.
- An SDK to assist SFe program developers with creating programs for the new format will be available with the version 4.00 final specification.
- For version 4.01, there will be an overhaul of the default modulators system, inspired by the [DMOD proposal by spessasus](https://github.com/davy7125/polyphone/issues/205).
- A MIDI lyrics specification for MIDI players will become available in version 4.02.
- We will negotiate with the Synthfont author Kenneth Rundt about getting the Synthfont Custom Features added for version 4.03.

# Section 2: Terms and abbreviations

## 2.1 Data structure terminology

The data structure terminology used in SFe32 version 4.00 is the same as the E-mu® SF2.04 standard.

* * *

## 2.2 Synthesis terminology

The synth terminology used in SFe32 version 4.00 is broadly the same as the E-mu® SF2.04 standard, with these additions:

- AWE64 - The successor to the famous AWE32, added things like waveguide synthesis. Used the EMU8000 synthesizer chip, like the preceding AWE32. Available in "Value" or "Gold" versions.

- DAHDSR - Stands for Delay, attack, hold, decay, sustain, release. The six-step envelope system used in SF and SFe.

- EMU10K1—The successor to the EMU8000, designed by E-mu® for the Creative Labs SB Live!.

- EMU10K2 - An update to the EMU10K1, designed by E-mu® for the Creative Labs SB Audigy.

- EMU20K1 - The successor to the EMU10K2, designed by E-mu® for the Creative Labs SB X-Fi.

- EMU20K2—An update to the EMU20K1, please refer [here](https://en.wikipedia.org/wiki/Sound_Blaster_X-Fi) for information on SB X-Fi cards that include it.

- Hold - The portion of the DAHDSR envelope after the attack portion, but before the decay portion starts.

- ROM samples - Obsolete feature used in legacy sound cards, most modern SF2 files do not use this feature.

- Sound Blaster® Live! — The successor to the AWE64, which improved the synthesizer chip to the EMU10K1, supporting modulators.

- Sound Blaster® Audigy - The successor to the SB Live!, containing the EMU10K2 chip.

- Sound Blaster® X-Fi - The successor to the SB Audigy, containing the EMU20K1 or EMU20K2 chip. Supports 24-Bit SoundFont® 2 files (2.04).

- Synth - Abbreviation of "Synthesiser," see "Synthesiser" in the 2.04 specification for more information.

- Version 3 - Refers to Werner SF3, a small upgrade to Soundfont® 2.04 created by Werner Schweer to allow an open source compression solution for SF programs (usually ogg, but can be any format).

- Version 4 - This new specification, based on SoundFont® 2.04 and Werner SF3, with a set of new features making it more realistic. Not to be confused with the unofficial Cognitone .sf4 file format, which is a variant of Werner SF3.


These changes:

- Articulation - Modulation of available parameters and usage of extra samples to produce expressive musical notes.
- Downloadable - SF version 2, 3 or SFe file obtained from the internet. (Old meaning referred to the obsolete ROM system)
- MIDI Bank - Groups of up to 128 presets, which can be selected by the two MIDI "Bank Select" control changes (CC00 and CC32).

And these removals:

- Preditor (refers to an old SF version 2 editor made by E-mu)

The terminology is also the same as SFe32 version 4.00.

* * *

## 2.3 Parameter terminology

The parameter terminology used in version 4 is broadly the same as the E-mu® SF2.04 standard, with these additions:

- Amplification - An increase in volume or amplitude of a signal.
- Flat - Said of a tone that is lower in pitch than another reference tone.

The terminology is also the same as SFe64 version 4.00.

# Section 3: RIFF and RF64 structure

## 3.1 General RIFF and RF64 file structures

### The RIFF format is the file format used in the SoundFont® 2.x and Werner SF3 standards, and in SFe32.

RIFF is created in building blocks known as "chunks".

Chunks are defined using this structure:

- A unique four character code (FourCC).
- "ckID": type of data in chunk
- "ckSize": size of chunk
- "ckDATA\[ckSize\]": the data inside the chunks, including pad bytes.

Chunks can be further divided into "sub-chunks."

Orders of chunks in all SF files are strictly defined, as in versions 2 and 3, and should be kept to.

* * *

## 3.2 Chunks and subchunks in version 4

Like SoundFont® 2.04, there are 3 main chunks:

1.  "INFO" Chunk: contains important information about the soundfont.

2.  "sdta" Chunk: A single sub-chunk containing audio samples.

3.  "pdta" Chunk: Nine sub-chunks (in the "Hydra" structure, named after a many-headed beast) containing the parameters about how the audio samples should be played. (According to E-mu, the hydra has nine heads. Cut one off, and another two grow.)

The three main chunks should appear in this order, and the nine sub-chunks of the "pdta" chunk should appear in the order described.

* * *

## 3.3 Error handling

The RIFF and RF64 formats have error checking features about:

- The size of the file
- The length of the chunks
- The length of the sub-chunks

Using this information, it is possible to check for damage to an SF(e) file:

- If any damage is detected due to such a mismatch, the file should be rejected as "Structurally Unsound."
- Like E-mu® SoundFont® 2.x and Werner SF3, developers can create programs which correct "Structurally Unsound" files of version 4 and later.
- A specification for such a program will be ready for 4.00.8.

# Section 4: RF64 file format of SFe32, version 4.00

## 4.1-4.4 File structure of version 4

Needs an update. This will be done for 4.00.8.

* * *

## 4.5 Type definitions

The type definitions are identical to those used in SoundFont® version 2.04.

* * *

## 4.5a File format extensions

SFe32 files should use file extension .SFE32 if incompatible with legacy SF players, but use .SF2 or .SF3 if compatible.

# Section 5: "info-list" chunk

## 5.1 "ifil" subchunk

### For compatibility

WORD wMajor = 2 or 3 (SFe32)

- wMajor=3 is used if the Werner SF3 sample format is used.
- Otherwise, use wMajor=2

WORD wMinor = 128 (SFe32)

- Legacy SF players might not support wMajor=4.
- SFe32 files technically appear as Version 2.128/3.128.

The size must be exactly 4 bytes. Reject files with an "ifil" subchunk that isn't 4 bytes as "Structurally Unsound".

### Using the specification version

Alternatively, the wMajor and wMinor can be set in the same way as the specification version, for example wMajor=4, wMinor=0 becomes wMajor=3, wMinor=128.

### In case of missing ifil subchunk

If the "ifil" subchunk is missing, either:

- Assume version 3.128 or 4.0.
- Reject the file as "Structurally Unsound".

* * *

## 5.1a Versioning rules

In SFe32, you can use two rules. Either:

- the value of wMajor remains 2 or 3, depending on if Werner SF3 is used
    - The value of wMinor counts up from 128.
    - It increases by one when a change is made to the format.
    - Later versions of the specification (4.01 onwards) will include a translation table to convert specification versions to SFe32 versions.
- the value of wMajor and wMinor correspond to the specification version

To signify that the SFe file has been created to a draft specification, please use the description.

* * *

## 5.2 "isng" subchunk

A new default isng sub-chunk value is used in SFe: "SFe32 version 4"

- SFe version 4 players should recognize this and remove the default velocity related filter used in SoundFont® 2.04.
- The ten "Default Modulators" will also be disabled by default. The Default modulation definition will be added in SFe version 4.01.
- In the case of a missing isng chunk, files with an ifil sub-chunk with wMinor >= 128, assume an isng sub-chunk value of "SFe32 version 4." Don't assume "EMU8000."

Reject anything not terminated with a zero byte, and assume the value "SFe32 version 4." Do NOT assume "EMU8000" by default.

* * *

## 5.3 "INAM" subchunk

This is mostly the same as in SoundFont® 2.04, but UTF-8 is now used instead of ASCII.

- The "INAM" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "GM Sound Set" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.4 "irom" subchunk

- Read the SoundFont® 2.04 specification for info on how to use ROM samples.
- The ROM emulator is optional in SFe32 programs.
- This subchunk will eventually be reused for other features in a future version of this specification.

* * *

## 5.5 "iver" subchunk

- Read the SoundFont® 2.04 specification for info on how to use ROM samples.
- The ROM emulator is optional in SFe32 programs.
- This subchunk will eventually be reused for other features in a future version of this specification.

* * *

## 5.6 "ICRD" subchunk

This is mostly the same as in SoundFont® 2.04, but UTF-8 is now used instead of ASCII.

- The "ICRD" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "October 17, 2024" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.7 "IENG" subchunk

This is mostly the same as in SoundFont® 2.04, but UTF-8 is now used instead of ASCII.

- The "IENG" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "SF Author" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.8 "IPRD" subchunk

This is mostly the same as in SoundFont® 2.04, but UTF-8 is now used instead of ASCII.

- The "IPRD" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "SFe32 Players" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.9 "ICOP" subchunk

This is mostly the same as in SoundFont® 2.04, but UTF-8 is now used instead of ASCII.

- The "ICOP" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "Copyright © All Rights Reserved." (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.10 "ICMT" subchunk

This is mostly the same as in SoundFont® 2.04, but UTF-8 is now used instead of ASCII.

- The "ICMT" subchunk contains a UTF-8 string of up to 65,536 bytes.
- Example of value: "This file contains 128 instruments and a drum kit." (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.11 "ISFT" subchunk

This is mostly the same as in SoundFont® 2.04, but UTF-8 is now used instead of ASCII.

- The "ISFT" subchunk contains a UTF-8 string of up to 256 bytes.
- Example of value: "SFe Editor version 4.00" (with appropriate zero bytes)

Reject anything not terminated with a zero byte. Do NOT reject the file as "Structurally Unsound."

* * *

## 5.12 "ISFe" subchunk

This would contain additional metadata for SFe specific features. Currently, in version 4.00, this is empty.

The first ISFe subchunk feature, the feature flags system, is planned for milestone 4.00.10.

* * *

&nbsp;

# Section 6: "sdta-list" chunk

## 6.1a "smpl" sub-chunk

You can omit this sub-chunk if you provide ROM samples.

- This contains one or more samples of audio in linearly coded 16-bit, signed, little endian words.
- No more leeway of 46 zero-valued samples is required after each sample.
- Before saving, SFe32 editors should insert this leeway. Otherwise, they might give a warning telling the user that loop and interpolation quality may be affected.
- If ROM samples are detected in SFe files, attempt to load them, even if this sub-chunk is missing.
- If this sub-chunk is missing, and no ROM samples are found, show an error message as mentioned in the program specification.

* * *

## 6.1b About compression in SFe32

To implement compression in your SFe32 bank, please use [Werner SF3](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format) compression encoding.

- Werner SF3 is widely used by the open source community.
- It is a standard that is being developed right now.
- There is no final specification, but the Fluidsynth team have a draft specification for Werner SF3.
- The goal is to make sure that these specifications are usable together.
- All SFe32 players must implement Werner SF3.
- Not all SFe32 files are required to implement Werner SF3 right now, but in the future it will become a requirement.
- Werner SF3 supports multiple different compression formats.
- The "scom" sub-chunk found in specification versions 4.00.3 and earlier is now obsolete.
- Incompatible SF compression formats (.sfark, .sfpack, .sf2pack, .sfq) are prohibited. You should use Werner SF3.

* * *

## 6.2a "sm24" and "sm32" sub-chunk

These sub-chunks are optional.

- The sm32 sub-chunk contains the least significant byte, and the sm24 sub-chunk contains the next least significant byte after sm32.
- Each sub-chunk is exactly half the size of the smpl sub-chunk.
- For every two bytes in the smpl sub-chunk, there is one byte in these sub-chunks.

![6.2a_1.png](../_resources/6.2a_1.png)

If these sub-chunks are present, they are combined with the other sub-chunks to create a sample with higher bitdepth.

- If the ifil version is below 2.04 (signifying an E-mu Systems® designed SoundFont® standard before 2.04), both sm24 and sm32 are ignored.

- If the ifil version is exactly 2.04 (signifying the E-mu Systems® designed SoundFont® 2.04 standard), only sm32 is ignored. The sm24 sub-chunk is still used.

- If these sub-chunks are not exactly half the size of the smpl sub-chunk (or otherwise invalid), the data should be ignored.

- If only the sm32 sub-chunk is invalid, the sm24 sub-chunk should still be loaded.

- However, if only the sm24 sub-chunk is invalid, both sub-chunks should be ignored.

- If the sm24 sub-chunk is ignored, the synthesizer should only attempt to render the first 16 bits of the samples contained within the smpl sub-chunk.

- If only the sm32 sub-chunk is ignored, the synthesizer should attempt to render both the smpl and sm24 sub-chunks, resulting in a 24-Bit sample.

- Due to the massive size, unpracticality and compatibility implications of 32-bit samples, use of the sm32 sub-chunk is not recommended! 

* * *

## 6.2b Using 8-bit samples

If the smpl sub-chunk is missing, but the sm24 or sm32 sub-chunks are present, 8-bit sample mode is to be activated.

- The sample depth is eight bits.
- The length of the sm24 sub-chunk should be rounded up to the nearest byte, as if the sub-chunk was being used with a smpl sub-chunk.
- If somehow, you've got both a sm24 and a sm32 sub-chunk, but no smpl sub-chunk, the sm24 sub-chunk is the most significant byte, and 16-bit sample playback is assumed.
- Editing software should give a warning if there is a sm24 and a sm32 sub-chunk but no smpl sub-chunk, and should convert it to a 2.01-compliant 16-bit format.
- This mode is only enabled if all samples are 8-bit. You cannot mix 8-bit and higher sample depths.
- SFe version 4 does not support non-standard sample bit depths (6-bit, 12-bit, 18-bit, etc.)

* * *

## 6.3 Looping rules

- No more leeway of eight samples is required.
- Before saving, SFe32 editors might give a warning about this leeway telling the user that loop and interpolation quality may be affected.

# Section 7: "pdta-list" chunk

## 7.1 "Hydra" structure

Like in E-mu Systems® SoundFont® 2.04, the format SFe32 version 4.00 is based on, the structure used is known as the "hydra" structure.

According to E-mu Systems®, a hydra has nine heads. Cut one off, and another two grow.

No major changes have been made to the structure itself. All nine of the sub-chunks are required. If any are missing, the file is "Structurally Unsound."

* * *

## 7.2 "phdr" sub-chunk

The size of this chunk is a multiple of 38 bytes.

Its structure is the same as in SF2.04.

### wPreset Changes

- In SoundFont® 2.04, bits 2–8 were used to select up to 128 instruments. Bits 1 and 9–16 were unused.
- Now, bits 10–16 can be used to select alternate banks.
- It's designed to be used with sysex or other commands corresponding to General MIDI extension resets.
- What bits 9–16 do in version 4:
    - Bit 9 remains reserved.
    - General MIDI™ one or two reset clears bits 10 and 11.
    - Roland® GS® reset clears bit 10 and sets bit 11.
    - Yamaha® XG® reset sets bit 10 and clears bit 11.
    - Roland® CM-64™/CM-32L™ reset sets bits 10 and 11.
    - Bit 12 is reserved for more MIDI commands in the future. For now, bit 12 should be written as clear.
    - Bits 13–16 will not be defined. The author of the SF may use these at will with their own MIDI commands.
    - MIDI sequencers will eventually be able to set or clear all bits from 10 to 16 using commands.
- It allows you to run multiple standards that may conflict with each other.

### wBank Changes

- Version 4.00.1 had a new field called wBank2.
- Now, wBank stores both m.s.b. and l.s.b. bank changes (CC00 and CC32), eliminating the need for wBank2.
- wBank is still a WORD. This change was possible as wBank is 16-bit, which is sufficient to store the 14-bit bank change space. We commend E-mu for being forward enough thinking to not use a CHAR/BYTE for bank selection.
- In SoundFont® 2.04, and SFe version 4.00.1, bit 1 was only used with bank 128 (for percussion), and bits 2–8 were used to select a single bank between 0 and 127. Bits 9–16 were unused.
- wBank is little endian.
- Now, bits 1 and are is a percussion toggle. If a bank/program change combination produces a different result for midi channel 10, bit 1 controls the percussion.
- File editors should warn the user if this issue is found.
- Bits 2–8 are now used to set the first bank change, and bits 10–16 are now used to set the second bank change.
- The default behavior is that bits 2–8 will set "m.s.b." (CC00) and bits 10–16 will set "l.s.b." (CC32), but version 4 compatible players should allow the user to swap CC00 and CC32 settings.
- Order in the phdr chunk in terms of wBank value.
- Summary:
    - Bit 1 = percussion toggle 1
    - Bit 2–8 = bank select m.s.b.
    - Bit 9 = percussion toggle 2
    - Bit 10-16 = bank selects l.s.b.

### Definitions of dwLibrary and dwGenre

Old 2.04 fields "dwLibrary" and "dwGenre" are now defined.

- "dwLibrary" is for the overall name of the set of files contained in a library of SFe, version 4 files.
    - For example, "SFe Collection!" (with appropriate zero bytes)
- "dwGenre" is for the genre of music which the files are optimized for.
    - For example, "Rock" (with appropriate zero bytes)
- "dwMorphology" has been left out of this draft specification. It will eventually be re-introduced.

### Do not access the final sfPresetHeader entry

The last sfPresetHeader entry shouldn't need to be accessed, apart from the uses described in the SF2.04 specification.

### This is a required sub-chunk

Files without a "phdr" sub-chunk are "Structurally Unsound."

* * *

## 7.3 "pbag" sub-chunk

This refers to the "Preset Bag" of the SFe file. This sub-chunk is a multiple of 4 bytes.

Its structure is the same as in SF2.04.

All values in this sub-chunk should be used as directed in the SF2.04 specification.

### This is a required sub-chunk

Files without a "pbag" sub-chunk are "Structurally Unsound."

* * *

## 7.4 "pmod" sub-chunk

The pmod sub-chunk is a multiple of 10 bytes.

The structure is very similar to SF2.04's PMod structure, with these differences:

### New options for the SFModulator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum, and all other enums, is two bytes in length.

### This is a required sub-chunk

Files without a "pmod" sub-chunk are "Structurally Unsound."

* * *

## 7.5 "pgen" sub-chunk

The pgen sub-chunk is a multiple of four bytes, like in SF2.04.

The structure and type definitions are the same as in SF2.04:

### New options for the SFGenerator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum is two bytes in length.

### This is a required sub-chunk

Files without a "pgen" sub-chunk are "Structurally Unsound."

* * *

## 7.6 "inst" sub-chunk

The inst sub-chunk is a multiple of 22 bytes.

### This is a required sub-chunk

Files without an "inst" sub-chunk are "Structurally Unsound."

* * *

## 7.7 "ibag" sub-chunk

This refers to the "Instrument Bag" of the SFe32 file.

This sub-chunk is a multiple of four bytes. This is like the pbag sub-chunk.

All values in this sub-chunk should be used as directed in the SF2.04 specification.

### This is a required sub-chunk

Files without an "ibag" sub-chunk are "Structurally Unsound."

* * *

## 7.8 "imod" sub-chunk

The imod sub-chunk is a multiple of 10 bytes, like the pmod sub-chunk.

The structure is very similar to SF2.04's imod structure, with these differences:

### New options for the SFModulator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum, and all other enums, is two bytes in length.

### Preset and instrument modulators

The Preset Modulator values are added to the Instrument Modulator values, and that is the final modulator used.

### This is a required sub-chunk

Files without an imod sub-chunk are "Structurally Unsound."

* * *

## 7.9 "igen" sub-chunk

The igen sub-chunk is a multiple of four bytes, like the pgen sub-chunk.

### New options for the SFGenerator enum

These options are listed elsewhere in the specification.

Legacy SF players which do not support these new enum options should ignore these new options.

This enum is two bytes in length.

### This is a required sub-chunk

files without an "igen" sub-chunk are "Structurally Unsound."

* * *

## 7.10 "shdr" sub-chunk

The shdr sub-chunk contains the headers for the sample data.

It is a multiple of 46 bytes.

### Sample Rate Limit Changes

- In SFe, sample rates (dwSampleRate) are stored as a 32-bit integer. This is the same behavior as seen in the legacy SoundFont® 2.04 format. This results in a theoretical maximum sample rate of 4,294,967,295 Hz.
- In the legacy SoundFont® 2.04 specification, E-mu suggested that sample rates of below 400 Hz or above 50,000 Hz should be avoided as some legacy hardware platforms may not be able to reproduce these sounds. This is not a limitation of the specification, but rather a limitation of legacy sound cards.
- Despite this, Creative did not use 16-bit integers for sample rate in SF 2.04. It is thus safe to use sample rates in excess of 50,000 Hz. If a sample rate of below 400 Hz or above 50,000 Hz is encountered, no attempt should be made to change the sample rate.
- A zero sample rate should be reset.

### sfSampleType and Werner SF3

Bit 4 of "sfSampleType" is reserved for Werner SF3 usage.

- Read the draft Werner SF3 specification for information!
- This specification is available at: [SoundFont3Format · FluidSynth/fluidsynth Wiki (GitHub.com)](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format)

The "sfSampleType" enum is two bytes in length.

### This is a required sub-chunk

Files without a "shdr" sub-chunk are "Structurally Unsound."

# Section 8: Enumerators

## 8.1.1 Kinds of generator enums

These are identical to SoundFont® 2.04.

* * *

## 8.1.2/3 Generator enums definitions

The Generator Enums used in SFe version 4.00, are the same as the SoundFont® 2.04 standard. SFe version 4.01 will include an overhaul of the modulator system, including new enums.

* * *

## 8.2.1 Source enum controller palettes

These are identical to SoundFont® 2.04.

* * *

## 8.2.2-3 Source Directions and Polarities

These are identical to SoundFont® 2.04.

* * *

## 8.2.4 Source Types

In SoundFont® 2.04, there are four sources.

* * *

## 8.3 Modulator transform enums

These are identical to SoundFont® 2.04 in SFe version 4.00, but SFe version 4.01 will include an overhaul of the modulator system, including new enums.

* * *

## 8.4.1-4 Default modulators 1-4

These have been removed, and no longer exist in SFe version 4.00, but the default modulator definition will be allowed in SFe version 4.01.

* * *

## 8.4.5-10 Default modulators 5-10

These are identical to SoundFont® 2.04.

* * *

## 8.5 Precedence, Absolute/Relative Values and Preset Level Availability of Generators.

The rules for precedence and absolute/relative values are identical to SoundFont® 2.04.

# Section 9: Parameters and synthesis model

## 9.1 SFe version 4 synthesis model

In SFe, the synthesis model will have massive improvements compared to the EMU8000-based synthesis model of SoundFont® 2.04 and Werner SF3 over time. Currently, it is identical to the synthesis model of SoundFont® 2.04, but version 4.01 will add the first improvements.

* * *

## 9.1.1 Sample-based oscillator

The method of operation is identical to SoundFont® 2.04.

* * *

## 9.1.2 Sample looping

The method of operation is identical to SoundFont® 2.04, but different types of looping will be added in a future version of SFe.

* * *

## 9.1.3 Filters

The method of operation is identical to SoundFont® 2.04, but different types of filters will be added in SFe version 4.01.

* * *

## 9.1.4 Final gain amplifier

The method of operation is identical to SoundFont® 2.04.

* * *

## 9.1.5 Effects Sends

The method of operation is identical to SoundFont® 2.04, but the chorus and reverb effects will be replaceable with different versions starting with SFe version 4.01.

* * *

## 9.1.6 Low Frequency Oscillators (LFOs)

There are two LFOs, which work in the same way as SoundFont® 2.04.

* * *

## 9.1.7 Envelope Generators

There are two envelope generators which work in the same way as SoundFont® 2.04.

* * *

## 9.1.8 Modulation interconnection

\[Insert figures of modulation interconnection\]

* * *

## 9.2 MIDI functions

Control Change #32 (Bank Select "LSB") has been modified to manipulate the high eight bits of the wBank value.

All other MIDI functions are unchanged from SoundFont® 2.04.

If a SoundFont® 2.00a file is loaded, see the legacy SoundFont® 2.04 specification for more details for handling of SoundFont® 2.00 files.

* * *

## 9.3 Parameter units

All of these are the same as SoundFont® 2.04.

* * *

## 9.4 SF Generator Model

This is the same as SoundFont® 2.04.

* * *

## 9.5 SF Modulator Model

- Modulators work in the same way as SoundFont® 2.04, but an update will be made in SFe version 4.01.
- \[New diagrams available soon\]

* * *

## 9.6 NRPN implementation

The NRPN implementation used by version 4.00 is identical to SoundFont® 2.04.

# Section 10: Error-handling

## 10.1 Structural errors

The error correction process for structural errors in SFe32 is largely similar to the process in older versions of the format.

* * *

## 10.1a Duplicated preset locations within files

This occurs when the file is structurally damaged or manually edited in a manner where more than one preset has the same value of wBank and wPreset (for instance, 015:000:081).

- In SoundFont® 2.04, the first preset in the location would be used by default, but the other presets would still be retained.
- Such other presets must be moved before they can be used.
- In SFe, the preset to be used is no longer necessarily the first one. Instead, selecting the correct preset (or combination of presets) to use will be permissible.
- Such a feature is optional, and if not implemented, the player should use the SF2.04 behavior in these cases (use the first preset found).
- Editors should warn the user if such presets are found.
- This behavior might change in future versions, so please take the "ifil" value, and later versions of this specification, into account. In particular, later versions of SFe will use the ISFe sub-chunk to determine this behavior.

* * *

## 10.1b Duplicated preset locations across files

This occurs when multiple files are loaded simultaneously (now a required feature for SFe), but some or all of the files have presets with identical wBank and wPreset values.

- Behavior was undefined in SoundFont® 2.04.
- This was because multiple file loading was not a standard feature mandated in the legacy SoundFont® standard.
- SF version 2 and 3 compatible software developers therefore had the liberty to implement multiple file loading; however, they wanted to.
- This edge case will now be defined in SFe.
- If multiple presets across loaded files have the same value of wBank and wPreset, then the preset to be used may be selectable from all the presets with the same bank location, depending on the player implementation. The preset to be used may also be a combination of multiple presets.
- Such a feature is also optional, and if not implemented, you can either use the first preset found, or you can combine all the presets.
- While initially intended to enable the creation of instruments with extremely large file size (beyond 4GiB), or use a massive number of generators (beyond 65536), with the SFe32 format, other methods, such as SiliconSFe Linking, are now preferred. However, such SFe32 files may not play correctly on legacy SF version 2 or 3 players.
- This behavior might change in future versions, so please note the "ifil" value, and later versions of this specification, into account. In particular, later versions of SFe will use the ISFe sub-chunk to determine this behavior.

* * *

## 10.2 Undefined chunks

SoundFont® 2.04 players should ignore SFe-specific sub-chunks, as prescribed by E-mu.

Also, SFe version 4.00 compatible players, which do not support future versions, should ignore sub-chunks which are used in future versions.

* * *

## 10.3 Unknown Enumerators

Any ifil versions of 4.01 or above may have unknown enumeration values for a version 4.00 player.

This is entirely expected, and if unknown enumeration values are found, the Generator/Modulator should be ignored.

* * *

## 10.4 Illegal Parameter Values

Illegal parameter values are handled as in SoundFont® 2.04.

* * *

## 10.5 Out of Range Values

Out of range values are handled as in SoundFont® 2.04.

* * *

## 10.5a Exceeded Maximum File Size Limit

This occurs when the user loads a file that is larger than the maximum size that the SFe program can accommodate.

- In the AWE32 and AWE64, the limit was dependent on the memory installed on the card, which was up to 28 MiB.
- Later, the sound cards allowed the user to load files with file sizes up to system memory.
- SFe has defined limits that are found in the separate program specification.
- If these limits are reached, you can reject loading of the file with an error, or attempt to load the file anyway.
- SFe programs should warn the user if processing was automatically done to a file to reduce the file size to be in range.
- If multiple files are loaded, and the limit is reached, the order of files to be loaded can be defined by the author of the SFe32 compatible software.

* * *

## 10.6 Missing Required Items

If required items are missing, it is handled as in SoundFont® 2.04.

* * *

## 10.7 Illegal Enumerators

Illegal enumerators are handled as in SoundFont® 2.04.

# Section 11: SiliconSFe

Traditional SiliconSF banks are provided for compatibility purposes only, but we are unaware of any shipping products using SiliconSF.

While it is optional, SFe32 players may include an AWE ROM emulator.

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

Read the SoundFont® 2.04 specification for information on how to make custom Silicon SF banks for older hardware.

A SiliconSFe specification will be available soon.

# Section 12: Glossary

This glossary is broadly the same as the SF2.04 specification's glossary, with these additions and changes:

- Amplification - An increase in volume or amplitude of a signal.

- Articulation - Modulation of available parameters and usage of extra samples to produce expressive musical notes.

- AWE64 - The successor to the famous AWE32, added things like waveguide synthesis. Use the EMU8000 synthesizer chip, like the preceding AWE32. Available in "Value" or "Gold" versions.

- BW64 - Broadcast Wave 64, used in the RF64 Header.

- DAHDSR - Stands for Delay, attack, hold, decay, sustain, release. The six-step envelope system used in SF and SFe.

- Downloadable - SF version 2, 3 or SFe file obtained from the internet. (Old meaning referred to the obsolete ROM system)

- EMU10K1 - The successor to the EMU8000, designed by E-mu® for the Creative Labs SB Live!.

- EMU10K2 - An update to the EMU10K1, designed by E-mu® for the Creative Labs SB Audigy.

- EMU20K1 - The successor to the EMU10K2, designed by E-mu® for the Creative Labs SB X-Fi.

- EMU20K2 - An update to the EMU20K1, please refer [here](https://en.wikipedia.org/wiki/Sound_Blaster_X-Fi) for information on SB X-Fi cards that include it.

- Flat - Said of a tone that is lower in pitch than another reference tone.

- Hold - The portion of the DAHDSR envelope after the attack portion, but before the decay portion starts.

- MIDI Bank - Groups of up to 128 presets, which can be selected by the two MIDI "Bank Select" control changes (CC00 and CC32).

- ROM samples - Obsolete feature used in legacy sound cards, most modern SF2 files do not use this feature.

- Sound Blaster® Live! - The successor to the AWE64, which improved the synthesizer chip to the EMU10K1, supporting modulators.

- Sound Blaster® Audigy - The successor to the SB Live!, containing the EMU10K2 chip.

- Sound Blaster® X-Fi - The successor to the SB Audigy, containing the EMU20K1 or EMU20K2 chip. Supports 24-Bit SoundFont® 2 files (2.04).

- Synth - Abbreviation of "Synthesiser," see "Synthesiser" in the 2.04 specification for more information.

- Version 3 - Refers to Werner SF3, a small upgrade to SoundFont® 2.04 created by Werner Schweer to allow an open source compression solution for SF programs (usually ogg, but can be any format).

- Version 4 - This new specification, based on SoundFont® 2.04 and Werner SF3, with a set of new features making it more realistic. Not to be confused with the unofficial Cognitone .sf4 file format, which is a variant of Werner SF3.