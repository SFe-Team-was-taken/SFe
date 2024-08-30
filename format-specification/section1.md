# Section 1: Introduction

## 1.1a Scope and purpose of this document

- This is a draft specification for the SFe file format, version 4, based on the famous E-mu Systems(r) Soundfont(r) 2.04, and Werner SF3 standards.
- It's intended to be a source of information on SFe.
- Using this document in conjunction with E-mu's provided documents and the Werner SF3 documents should allow you to make files that support SFe.
- All features from version 2.04 will be retained.

* * *

## 1.1b Important differences from the 2.04 document

- Important: This is not a standalone document; it refers to both the SF2.04 and Werner SF3 technical specifications.
- Important: This document is not official, and not created by E-mu. If you want this to be removed, we will remove it.
- For copyright reasons, we cannot copy information from the original standard, except for what is required to interpret this document and what is allowed under fair use. For more detailed information, we will provide an external link to the SF 2.04 standard, here. [SF 2.04 standard specification on Freepats website](https://freepats.zenvoid.org/sf2/sfspec24.pdf)
- Draft of the Werner SF3 specification: [SoundFont3Format · FluidSynth/fluidsynth Wiki (github.com)](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format)

* * *

## 1.2 Document organisation

The sections in this specification map to the E-mu Systems(r) Soundfont(r) 2.04 specification document.

- Like the version 2.04 specification, section 1 and 2 will give introductory information about SFe.
    
- Sections 3-8 provide detailed information about the new third generation structure.
    
- Section 9 shows the next generation synthesis engine, improved significantly from the engines that AWE32 and its relatives used.
    
- Section 10 describes any error handling which is needed when opening SFe files.
    
- Section 11 describes legacy ROM methods of storing an SFe32 file.
    
- Section 12 is a glossary of most terms in this draft specification.
    

New sections may be added in the future, depending on if radical changes are made to the format.

* * *

## 1.3 SFe objectives

### The SF-enhanced (SFe) standard, version 4, has been created to provide a successor to E-mu Systems(r)'s Soundfont(r) 2.04 standard, with many different new features which are required to increase realism of virtual instrument banks further.

An all-new 64-bit version, called SFe64, is based on the RIFF64 (RF64) standard, which is very similar to the 32-bit RIFF standard.

- The file size limit is 16 EiB, and this format has changed many of the data types from 16-bit to 32-bit, and 8-bit to 16-bit.
- Parameter size limits have increased from 65,536 to 4,294,967,296.
- Large files requiring larger size limits must use SFe64.
- SFe64 is not completely compatible with SFe32. Legacy SF players (like AWE32) will not playback SFe64 files.
- However, this new version will be easily convertible to SFe32, so SFe64 files with a file size of below 4GiB can be converted with little to no quality loss.
- Also, programs that are designed to create existing SF2 files can easily be adapted to 64-bit with the SFe64 format.
- SFe64 will allow creators of sound banks to replace split banks with a large number of SF2 files (and supporting files like SFLISTs), with very large, single, ready-to-use files, where all samples and instruments can be shared in the sound bank's presets.

A backwards compatible 32-bit version, called SFe32, based on the famous and reliable RIFF standard, adds many extra features, while striving for compatibility with legacy SF players. It will also be compatible with existing software that implements Werner SF3 compression.

- In this version, the file size limit remains 4GiB, and the data types have stayed the same.
- There will be a few new modulators, and some nifty new features like round robin sample switching.
- ROM features for legacy sound cards will also be kept, to allow the ROM samples inside these old sound cards to be used with the new features of version 4.
- SFe32 will be completely compatible with legacy SF players\*. All that is needed is usage of the sf2 extension, and it should be possible to load an SFe32 file, version 4, on existing software.
- We will not release a version of SFe32 if the resulting features break the forward compatibility of legacy soundfont players.
- SFe32 will impart critical features that are not found in the current versions 2 and 3 format to bring the popular install base of the SF2/SF3 format forward to the 21st century and beyond; it will also act as a stepping stone between SF2/SF3 and SFe64, which is our vision of the monolithic sample library of the future.
- Specific versions of programs that support SFe32 will not be required, as the SFe64 standard is designed to allow SFe32 files to be parsed as SFe64 and play without issues.
- SFe32 compatible players require a certain standard of features, which is in the separate SFe program specification.

\*All legacy SF players that conform to the standard SF 2.04 spec. Compatibility is not guaranteed if the player fails to correctly implement said spec.

* * *

## 1.4 The background of the SF format

SoundFont(R) 1 refers to the proprietary version of the format used by the Creative Labs AWE-32 sound card released in 1994.

- SoundFont(R) 1 files had a file extension of .SBK and can not be used by many SF 2.x programs.
- This is the version used in the Creative Labs DOS drivers.
- Creative Labs is the brand name of the company "Creative Technology Ltd".
- As the specification for SF 1 was never released, we don't know how SF 1 files were structured.

Creative Labs decided to release the specification to the public with version 2.00 in 1996 (specification date October 1995).

- This requires the Windows drivers for use in older Creative Labs Sound Blaster(r) cards.
- DOS drivers can only use .SBK (SoundFont(R) 1) files.

In 1998, modulators were added in the SoundFont(R) 2 version 2.01 (specification date August 1997).

- It is backwards compatible with 2.0.
- This was designed for use in the new SB Live! card (EMU10K1).

Finally, in 2005, Version 2.04 was released, with 24 bit support (specification date September 2002).

- It is backwards compatible with 2.01.
- This was designed for the SB X-Fi.

The format was then abandoned by E-mu. Creative Technology Ltd is still around however; you can buy shares in said company.

Current Creative Labs sound cards do not support the SF2 format; the Audigy RX from 2013 was the last model that supported the format. Newer cards, for instance the AE-9, use an "off-the-shelf" or newer Creative Labs sound processor that no longer uses wavetable sound synthesis.

At an unknown time, Kenneth Rundt, the author of SynthFont and a series of products based on it, added some custom features, ported over from the DLS format:

- Always play the sample to the end
- Velocity to volume envelope attack (from DLS)
- Velocity to modulation envelope attack (from DLS)
- Vibrato lfo to volume (from DLS)

Werner Schweer found a way to compress SoundFont(R) 2 files (with the lossy Vorbis format).

- The resulting format was known as SF3.
- It is commonly used by open source programs.
- This is the reason why this format is not called .SF3 (it was in 4.00.1, but after **feedback by derselbst** and **mawe42** on Github, we changed it to SFe32 and SFe64).
- SFe files will be compatible with Werner SF3 for compression.

Another development was done by Cognitone, which created an open source program that can losslessly compress SoundFont(R) 2 files (with FLAC).

- This was unofficially called SF4.
- This is intended to be the true version 4, as Cognitone SF4 seems to not have been as widespread as SF3.
- SF4 has also been rejected by the Werner SF3 community as too loosely defined.

Finally, stgiga found out that many programs don't actually mind RIFF64 (RF64) files.

- RIFF64 files have a much larger size limit than 32-bit RIFF files.
- It gives us a new horizon to experiment with longer, higher quality samples.
- There are also many other advantages of the RIFF64 format.

And this is where we stand now.

* * *

## 1.5 Improvements and enhancements

SFe (version 4) is designed for future improvements.

- These will be done in a more liberal way than the conservative manner of the Soundfont(r) 2 updates that E-mu has done.
- Some improvements will only be available in SFe64.
- SFe32 version 4 will have a reduced set of improvements, as it is designed to be completely backward compatible with SF2.04.
- No version of SFe32 will become incompatible with fully compliant SF2.04 software.
- Eventually, we will permanently freeze SFe32, only if and when SFe64-compatible software has reached significant acceptance.
- After the feature freeze, SFe32 will remain a dependable and stable format for software development to be based on.
- SFe64 version 4 forgoes all the limitations created by the EMU8000 sound processor, and Sound Blaster(r) cards, and therefore will have more improvements.
- To avoid over-stress of developers of the SFe Team, as well as SFe instrument banks, features will be spread out across versions. We hope to release a new version every 3-5 years.
- SFe64 development can be done in tandem with SFe32.

* * *

## 1.5a Future plans

The features for version 4.00 have been frozen after the release of version 4.00.4. This doesn't mean that we're done with SFe, in fact this is only the beginning of the format's development.

We decided to do a feature freeze for version 4.00 to make sure that SFe program developers have a reasonable set of features to implement. If we add too many features, it can overwhelm developers.

Here are a few things that are planned for SFe:

- For SFe draft specification version 4.00.6, we are planning to introduce the SFe file repair program specification.
- An SDK to assist SFe program developers with creating programs for the new format will be available with the version 4.00 final specification.
- For version 4.01, there will be an overhaul of the default modulators system, inspired by the [DMOD proposal by spessasus](https://github.com/davy7125/polyphone/issues/205).
- We will negotiate with the Synthfont author Kenneth Rundt about getting the Synthfont Custom Features added to a future version of SFe.