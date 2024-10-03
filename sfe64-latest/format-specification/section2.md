# Section 2: Terms and abbreviations

## 2.1 Data structure terminology

The data structure terminology used in version 4 is broadly the same as the E-mu(r) SF2.04 standard, with these additions:

- BW64 - Broadcast Wave 64, used in the RF64 Header.
- RF64 - See "RIFF64".
- RIFF64 - A format mostly compatible with RIFF, SF2.04's basic file format. This is 64-bit, unlike RIFF, which is 32-bit. Therefore, the maximum file size is above 4 gigabytes in size.

* * *

## 2.2 Synthesis terminology

The synth terminology used in SFe64 version 4.00 is broadly the same as the E-mu(r) SF2.04 standard, with these additions:

- AWE64 - The successor to the famous AWE32, added things like waveguide synthesis. Used the EMU8000 synthesiser chip, like the preceding AWE32. Available in "Value" or "Gold" versions.
    
- DAHDSR - Stands for Delay, attack, hold, decay, sustain, release. The six step envelope system used in SF and SFe.
    
- EMU10K1 - The successor to the EMU8000, designed by E-mu(r) for the Creative Labs SB Live!.
    
- EMU10K2 - An update to the EMU10K1, designed by E-mu(r) for the Creative Labs SB Audigy.
    
- EMU20K1 - The successor to the EMU10K2, designed by E-mu(r) for the Creative Labs SB X-Fi.
    
- EMU20K2 - An update to the EMU20K1, please refer [here](https://en.wikipedia.org/wiki/Sound_Blaster_X-Fi) for information on SB X-Fi cards that include it.
    
- Hold - The portion of the DAHDSR envelope after the attack portion, but before the decay portion starts.
    
- ROM samples - Obsolete feature used in legacy sound cards, most modern SF2 files do not use this feature.
    
- Soundblaster(r) Live! - The successor to the AWE64, which improved the synthesiser chip to the EMU10K1, supporting modulators.
    
- Soundblaster(r) Audigy - The successor to the SB Live!, containing the EMU10K2 chip.
    
- Soundblaster(r) X-Fi - The successor to the SB Audigy, containing the EMU20K1 or EMU20K2 chip. Supports 24-Bit Soundfont(r) 2 files (2.04).
    
- Synth - Abbreviation of "Synthesiser", see "Synthesiser" in the 2.04 specification for more information.
    
- Version 3 - Refers to Werner SF3, a small upgrade to Soundfont(R) 2.04 created by Werner Schweer to allow an open source compression solution for SF programs (usually ogg, but can be any format).
    
- Version 4 - This new specification, based on Soundfont(r) 2.04 and Werner SF3, with a set of new features making it more realistic. Not to be confused with the unofficial Cognitone .sf4 file format, which is a variant of Werner SF3.
    

These changes:

- Articulation - Modulation of available parameters and usage of extra samples to produce expressive musical notes.
- Downloadable - SF version 2, 3 or SFe file obtained from the internet. (Old meaning referred to the obsolete ROM system)
- MIDI Bank - Groups of up to 128 presets, which can be selected by the two MIDI "Bank Select" control changes (CC00 and CC32).

And these removals:

- Preditor (refers to an old SF version 2 editor made by E-mu)

The terminology is also the same as SFe32 version 4.00.

* * *

## 2.3 Parameter terminology

The parameter terminology used in version 4 is broadly the same as the E-mu(r) SF2.04 standard, with these additions:

- Amplification - An increase in volume or amplitude of a signal.
- Flat - Said of a tone that is lower in pitch than another reference tone.

The terminology is also the same as SFe32 version 4.00.