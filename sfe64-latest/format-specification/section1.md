# Section 1: Introduction

## 1.1a Scope and purpose of this document

- This is a draft specification for the SFe64 file format, version 4.00, based on the famous E-mu Systems(r) Soundfont(r) 2.04, and Werner SF3 standards.
- It's intended to be a source of information on SFe64.
- To create files that support SFe64, you will need:
    - The SFe64 format, compatibility and program specifications
    - The SFe32 format, compatibility and program specifications
    - E-mu's provided documents for SF 2.04 ([sfspec24.pdf](https://freepats.zenvoid.org/sf2/sfspec24.pdf))
    - The Werner SF3 specification ([draft by FluidSynth](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format))
- All features from version 2.04 will be retained.

* * *

## 1.1b Important differences from the 2.04 document

- This is not a standalone document; it refers to both the SF 2.04 and Werner SF3 technical specifications.
- This document is unofficial, and was not created by E-mu. If you want this to be removed, we will remove it, but we hope that this is because you have your own update to the SF format ready.
- For copyright reasons, we cannot copy information from the original standard, except for what is required to interpret this document and what is allowed under fair use.

* * *

## 1.2 Document organisation

The sections in this specification map to the E-mu Systems(r) Soundfont(r) 2.04 specification document.

- Like the version 2.04 specification, section 1 and 2 gives introductory information about SFe64.
- Sections 3-8 provide detailed information about the updates made to the SFe64 structure.
- Section 9 shows the synthesis engine.
- Section 10 describes any error handling which is needed when opening SFe64 files.
- Section 11 describes legacy ROM methods of storing an SFe64 file.
- Section 12 is a glossary of most terms in this draft specification.

New sections may be added in the future, depending on if radical changes are made to the format.

* * *

## 1.3 SFe objectives

### The SFe64 standard, has been created to provide a 64-bit successor to E-mu Systems(r)'s Soundfont(r) 2.04 standard, enabling file sizes of greater than 4 GiB, in addition to further building on the features of SFe32.

- The file size limit is 16 EiB.
- Large files requiring larger size limits must use SFe64.
- Programs that are designed to create existing SF2 files can easily be adapted to 64-bit with the SFe64 format.
- SFe64 will allow creators of sound banks to replace split banks with a large number of SF2 files (and supporting files like SFLISTs), with very large, single, ready-to-use files, where all samples and instruments can be shared in the sound bank's presets.
- SFe64 compatible players require a certain standard of features, which is in the separate SFe program specification.

* * *

## 1.4 The background of the SF format

SoundFont(R) 1 refers to the proprietary version of the format used by the Creative Sound Blaster(r) AWE32 sound card released in 1994.

- SoundFont(R) 1 files had a file extension of .SBK and can not be used by many SF 2.0x programs.
- This is the version used in the Creative DOS drivers.
- Creative is the brand name used by the company "Creative Technology Ltd".
- As the specification for SF 1 was never released, we don't know how SF 1 files were structured.

Creative decided to release the specification to the public with version 2.00 in 1996 (specification date October 1995).

- This requires the Windows drivers for use in older Sound Blaster(r) cards.
- DOS drivers can only use .SBK (SoundFont(R) 1) files.

In 1998, modulators were added in the SoundFont(R) 2 version 2.01 (specification date August 1997).

- It is backwards compatible with 2.00.
- This was designed for use in the new SB Live! card (EMU10K1).

Finally, in 2005, version 2.04 was released, with 24-bit support (specification date September 2002).

- It is backwards compatible with 2.01.
- This was designed for the SB X-Fi.

The format was then abandoned by E-mu. Creative Technology Ltd is still around however as a public company.

Current Creative Labs sound cards do not support the SoundFont(R) format; the Audigy RX from 2013 was the last model that supported the format. Newer cards, for instance the AE-9, no longer use wavetable sound synthesis.

At an unknown time, Kenneth Rundt, the author of SynthFont and a series of products based on it, added some custom features, mostly ported over from the DLS format:

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

Finally, stgiga found out that many programs don't actually mind RIFF64 (RF64) files. This is the purpose of the SFe64 format.

- RIFF64 files have a much larger size limit than 32-bit RIFF files.
- It gives us a new horizon to experiment with longer, higher quality samples.
- There are also many other advantages of the RIFF64 format.

This is where we stand right now.

* * *

## 1.5 Improvements and enhancements

SFe (version 4) is designed for future improvements.

- These will be done in a more liberal way than the conservative manner of the Soundfont(r) 2 updates that E-mu has done.
- Some improvements will only be available in SFe64.
- SFe64 is not affected by limitations created by the EMU8000 sound processor, and Sound Blaster(r) cards, and therefore will have more improvements.
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