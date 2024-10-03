# SF-enhanced 64-bit (SFe64) specification

## Version 4.00.6 (draft specification) - Revision A

Copyright 2020-2024 SFe Team

Based on the abandoned E-mu spec, which is copyright 1994-2002 E-mu Systems Inc.

* * *

## 0.1 Revision history

|     |     |     |
| --- | --- | --- |
| Revision | Date | Description |
| This version | October 3, 2024 | Added milestone classification for some draft specifications in 0.1a  <br>Removed all SFe32-specific information, renamed to SFe64 spec  <br>Renamed 3.1a to 3.1, 6.1a to 6.1, 6.1b to 6.1a, 6.2a to 6.2, and 6.2b to 6.2a, for consistency  <br>Delayed modulator update to version 4.01  <br>Removed 7.1a, because it's not relevant to versions before 5.00  <br>Added LSB to example value in 10.1a  <br>Added more information about future plans  <br>Reworked SFe64 to be a simple 64-bit extension to SFe32 for now, features will come later |
| 4.00.5c | September 2, 2024 | Added clarification for timeframe in which 0.4 will be filled out  <br>Rewritten 1.1a to be clearer, moving links from 1.1b  <br>Removed redundant "important" words in 1.1b  <br>Moved some compatibility info from sections 1.3 and 3.1 to compatibility spec  <br>ROM samples no longer listed as deprecated in 3.2, 5.4, 5.5 and 6.1a  <br>Error handling plans for version 4.00.6 added in 3.3  <br>Fixed capitalisation in 4.5  <br>Added section 4.5a for file format extensions, removed .sf32 and .sf64  <br>Removed isfe reference for 5.1, SFe32 programs can determine WernerSF3 with wMajor=3  <br>Fixed reference to compatibility spec in 5.1a, compatibility spec is not used in SFe64  <br>Rewritten 5.2 to make it clearer, and to mention default modulator definitions for 4.01.  <br>Added heading 3 in formatting of section 7 and section 7.1a for subchunk size alignment.  <br>Removed reverb/chorus definitions in 8.1.2, 8.1.3 and 9.1.5 (will be restored in 4.01)  <br>Fixed some other typos and added a few other clarifications |
| 4.00.5b | September 1, 2024 | Clarified information about sample rates in section 7.10 |
| 4.00.5a | August 30, 2024 | All remaining SF32/SF64 references should now be renamed to SFe32/SFe64  <br>Added ROM sample specification for the AWE ROM emulator  <br>Replaced draft number references with the new versioning system  <br>Added clarification for the compatibility specification versioning  <br>Fixed mistake in INFO chunk information in the compatibility specification  <br>Clarified that this document is not created by E-mu  <br>Added placeholder for the SF Server link  <br>Specific version number added to title  <br>Added instructions to compatibility spec about how to handle incompatible compression  <br>Error messages modified to remove scom reference and fix version 3 reference to version 4  <br>Added section 1.5a to mention future plans for the SFe format  <br>Added 0.1a to describe specification versioning  <br>Removed unnecessary information about Creative Technology  <br>Proprietary compression formats are now forbidden in the program specification  <br>Added references to SFe Team; a list of developers can be found in 0.3a.  <br>Next version for release by early 2025 will have the SFe file repair program specification |
| 4.00.4 | July 4, 2024 | Clarified about legacy compliance and TSC in section 3.2.  <br>Added more clarification in revision history  <br>8-bit mode information updated again  <br>Added info about how SFe32 can be parsed as SFe64  <br>More information about the pdta structure added  <br>Real time synthesis is no longer mandatory  <br>Renamed to version 4 and updated versioning scheme  <br>Added preliminary Werner SF3 compatibility  <br>Removed scom sub-chunk  <br>For now, removed increased character limits in SFe32.  <br>Changed sleaf's name on the contact.  <br>Added information on bank select and TSC mode  <br>Added the isfe sub-chunk for SFe64  <br>One mention of "back and forth" now "bidirectional"  <br>Added and clarified some terms in glossary  <br>Stated that incompatible compression is no longer allowed in 6.1b.  <br>Renamed SF32 and SF64 to SFe32 and SFe64.  <br>Added clarification of "SFe format developers" in 1.5.  <br>Moved compatibility information to the compatibility specification.  <br>Added 5.1a to describe ifil sub-chunk versioning. |
| 4.00.3 | September 6, 2022 | Added clarification  <br>Renamed 32-bit SF version 3 to SF32  <br>Overall format has been renamed to SFe (SF enhanced)  <br>wBank bit 9 is no longer reserved.  <br>Silicon SF banks for SF64  <br>Added CM reset  <br>Changed isng value  <br>Fixed some pdta sub-chunks for SF64  <br>Corrected sfSampleType reference from bit 15 to bit 16.  <br>Renamed "back and forth" to "bidirectional"  <br>Changed "improved" to "fixed" in revision log  <br>Added a nicer diagram (can you find it?)  <br>Fixed extraneous reference to wBank2 in section 4.  <br>Modified information about the scom sub-chunk.  <br>8-bit mode information updated |
| 4.00.2 | July 22, 2022 | Renamed 64-bit SF3 to SF64 version 3  <br>32-bit SF3 is now 32-bit SF version 3  <br>Changed ASCII to UTF-8  <br>Fixed the wPreset and wBank (removed wBank2) |
| 4.00.1 | April 12, 2020 | First version |
| (2.04) | (September 10, 2002) | (Last version authored by E-mu until format abandoned) |

* * *

## 0.1a Specification Versioning

Final specifications have version numbers in the format x.yyL, where x and y are numbers and l is a letter:

- x is incremented when a change in the SFe64 format is made in a way that makes the resulting files incompatible with the previous version.
- y is incremented when there are new features added to either the SFe64 or the SFe32 format.
- SFe64 should not skip "y" versions. There will not be SFe32-only feature additions.
- L is incremented when there are small changes made to the specification, if L is absent then assume that it is "a".
- An example of a final specification version would be 4.00.

Draft specification milestones have version numbers in the format x.yy.zL, where x, y and z are numbers and L is a letter. In this case, the versioning works similarly to a final specification, but with these changes:

- z is incremented when the draft undergoes a larger change, or large updates are made to the software.
- L is incremented when there are small changes, but only when pointed out by others.
- An example of a draft specification version would be 4.00.5.

During the development of specifications, version numbers will be in the format x.yy.aaaabbccL, where x, y, z, a, b and c are numbers, and L is a letter. The versioning is similar to final specifications and milestone drafts, but aaaabbcc is the day in which the specification was updated, and L is incremented when updated.

The revision history table refers to development versions as "This version" and includes the cumulative changes made to the specification since the last milestone revision.

* * *

## 0.2 Disclaimers

We don't own the rights to use the term "Soundfont", so the term SF is used instead.

The trademark rights to the term "Soundfont" belong to Creative Technology Ltd.

That being said, "soundfont" is rapidly becoming a genericised word via the actions of the VGM (video game music) and lightsaber communities (despite the lightsaber community not using .sf2 files, and misusing the term for another format).

We urge rights holders (Creative Technology Ltd.) to prevent the lightsaber community from appropriating the trademark for their unrelated format.

All excerpts from the SF 2.04 specification are copyrighted by E-mu Systems or Creative Technology Ltd, and are only used for reference. Everything should fall under fair use rights.

We are confident that the base file format is not copyrightable, but we are able to take this document down if necessary.

This is a draft. Expect errors, and feel free to report them. sleaf has access to a computer with an Sound Blaster X-Fi Titanium, so she will be able to test or reproduce any issues found on real hardware.

Do not use "draft" specifications (version number x.yy.zL) to base final products on. Always refer to a "final" specification (version number x.yyL).

* * *

## 0.3 Updates and comments

The website "soundfont.com" is dead (last archive.org snapshot we could found was 2012/13), and the provided email on the SF 2.04 spec probably doesn't work, so contact the SFe Team:

- GitHub: https://github.com/SFe-Team-was-taken

A link to the SF Server Discord will be provided soon.

* * *

## 0.3a SFe Team

SFe Team members:

- sleaf (she/her) | Discord - @tanukilvia | Email - sylvialeaf6284@gmail.com
- Stgiga (they/them) | Discord - @stgiga

Thanks to these people for suggestions: derselbst, mawe42, Saga, spessasus

Want to join the SFe Team? Please contact sleaf using the contacts in section 0.3.

* * *

## 0.4 Table of contents

The table of contents will be added when we can confirm that no more sections will be added to version 4.00 of the SFe specification.

* * *

## 0.5 Illustrations

\[Again this is coming in a later draft.\]