# Section 12: Glossary

This glossary is broadly the same as the glossary in `SFSPEC24.PDF`, with these additions and changes:

- Articulation - Modulation of available parameters and usage of extra samples to produce expressive musical notes.
- AWE64 - The successor to the famous AWE32, adding features such as waveguide synthesis. Used the EMU8000 synthesizer chip, like the preceding AWE32. Available in "Value" or "Gold" versions.
- Branch - A subdivision of a tree structure containing either sub-branches or leaves that include values.
- Case-insensitive - Indicates that a UTF-8 character or string treats alphabetic characters of upper or lower case as identical.
- Case-sensitive - Indicates that a UTF-8 character or string treats alphabetic characters of upper or lower case as distinct.
- Cognitone SF4 - An incompatible modification to Werner SF3 to allow support for FLAC audio compression. Because it is considered an incompatible compression format, usage is not allowed in SFe. (Updated in 4.0b)
- DAHDSR - Stands for Delay, attack, hold, decay, sustain, release. The six-step envelope system used in SF and SFe.
- Downloadable - legacy SF2.0x, Werner SF3 or SFe file obtained from the internet. (Old meaning referred to the obsolete ROM system)
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
- Quirk - Any player-specific function that is automatically enabled and modifies the behaviour of any numeric parameters used by legacy SF2.0x, including preset locations, parameters, units, modulators or NRPNs.
- Quirks mode - A mode in an SFe-compatible player that enables the implementation quirks.
- RIFF-type format - Formats similar to RIFF (Resource Interchange File Format), see "RIFF" in `SFSPEC24.PDF` for more information.
- RIFS - "RIFF-like static 64-bit", a simple 64-bit RIFF-like format that uses the exact same syntax as RIFF but with 8-byte chunk size instead of 4-byte. (Update 17)
- ROM samples - Obsolete feature used in legacy sound cards, most modern SF2 files do not use this feature.
- SB - Abbreviation of "Sound Blaster®". For example, "SB X-Fi".
- SFe - A family of enhancements to the SoundFont® 2.04 formats, unofficially created after E-mu/Creative abandoned the original format. May not be structurally compatible with legacy SF2.04.
- SFe 4 - This new specification, based on SoundFont® 2.04 and Werner SF3, with a set of new features making it more realistic. Not to be confused with the incompatible Cognitone SF4 file format.
- SFe-compatible - Indicates files, data, synthesisers, hardware or software that conform to the SFe specification.
- SFe Compression - The compression system based on Werner SF3 that SFe programs should be compliant with.
- Sound Blaster® Live! - The successor to the AWE64, which improved the synthesizer chip to the EMU10K1, supporting modulators.
- Sound Blaster® Audigy - The successor to the SB Live!, containing the EMU10K2 chip.
- Sound Blaster® X-Fi - The successor to the SB Audigy, containing the EMU20K1 or EMU20K2 chip. Supports 24-Bit SoundFont® 2 files (2.04).
- Static RIFF - Any RIFF-type format with a fixed chunk size field width, including RIFF or RIFS. See "RIFF-type format", "RIFF" and "RIFS".
- Synth - Abbreviation of "Synthesiser," see "Synthesiser" in `SFSPEC24.PDF` for more information.
- Tree structure - A structure consisting of branches and leaves.
- Vorbis - A lossy audio compression format commonly used in open-source software. The basic compression format that most Werner SF3 and SFe-compatible software should be expected to implement.
- Werner SF3 - A small upgrade to SoundFont® 2.04 created by Werner Schweer to allow an open source compression solution for SoundFont® programs. Standardised as SFe Compression.
