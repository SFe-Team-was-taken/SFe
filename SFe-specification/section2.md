# Section 2: Terms and abbreviations

## 2.1 Data structure terminology

The data structure terminology used in version 4 is broadly the same as the E-mu(r) SF2.04 standard, with these additions:

- BW64 - Broadcast Wave 64, used in the RF64 Header.
- LONG - Data structure element of 32 Bits containing a signed value from -2,147,483,648 to 2,147,483,647.
- LONG LONG - Data structure element of 64 bits containing a signed value from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.
- QWORD - 64-Bit data structure containing an unsigned value from zero to 18,446,744,073,709,551,615.
- RF64 - See "RIFF64".
- RIFF64 - A format almost compatible to RIFF, SF2.04's basic file format. This is 64-bit, unlike RIFF, which is 32-bit. Therefore, the maximum file size is above 4 gigabytes in size.

* * *

## 2.2 Synthesis terminology

The synth terminology used in version 3 is broadly the same as the E-mu(r) SF2.04 standard, with these additions:

- AWE64 - The successor to the famous AWE32, added things like waveguide synthesis. Used the EMU8000 synthesiser chip, like the preceding AWE32. Available in "Value" or "Gold" versions.
    
- Bandpass - Filter which attenuates both low and high frequencies.
    
- Bandreject - See "notch filter"
    
- Compressor - Effect which reduces the dynamic range of a sound.
    
- DAHDSR - Stands for Delay, attack, hold, decay, sustain, release. The six step envelope system used in SF and SFe.
    
- Distortion - Method of modifying the sound of an instrument (commonly a guitar) by distorting the sound. Creates a harsh and cutting sound.
    
- EMU10K1 - The successor to the EMU8000, designed by E-mu(r) for the Creative Labs SB Live!.
    
- EMU10K2 - An update to the EMU10K1, designed by E-mu(r) for the Creative Labs SB Audigy.
    
- EMU20K1 - The successor to the EMU10K2, designed by E-mu(r) for the Creative Labs SB X-Fi.
    
- EMU20K2 - An update to the EMU20K1, please refer [here](https://en.wikipedia.org/wiki/Sound_Blaster_X-Fi) for information on SB X-Fi cards that include it.
    
- EQ - Abbreviation of "equalisation" or "equaliser", see "Equalisation" for more information.
    
- Equalisation - Method of altering a sound, involves adjusting the volume of certain frequency responses.
    
- Filter depth - A parameter used in a filter, determines how quickly the frequency response falls off after the cutoff frequency has been reached. Measured in poles or dBa.
    
- Flanger - An effect which modulates the sound, thickening the sound, similarly to chorus.
    
- FM - Abbreviation of "Frequency modulation", see "Frequency Modulation".
    
- Frequency Modulation - A method of synthesis more correctly called phase modulation, where a modulator changes the frequency of a carrier over time.
    
- Highpass - Filter which attenuates low frequencies and not high frequencies.
    
- Hold - The portion of the DAHDSR envelope after the attack portion, but before the decay portion starts.
    
- Notch filter - Filter which attenuates the cutoff frequency and the frequencies around it. Also called a bandreject filter.
    
- Overdrive - An effect which is similar to distortion.
    
- Phaser - An effect which modulates the sound, causing the sound to be modified in a manner which is called "phasing".
    
- Rolloff - See "Filter depth" for more information.
    
- ROM samples - Obsolete feature used in legacy sound cards, most modern SF2 files do not use this feature.
    
- Rotary Effect - Simulates a famous speaker, commonly used with drawbar organs. Available in both fast and slow variations.
    
- Sample and hold - LFO type where the value of the modulated parameter changes to a random value between two values at a constant rate.
    
- Sine - Waveform which is represented by the function sin(t). Has no harmonic overtones.
    
- Square - Waveform which switches between two states at a constant rate.
    
- Subtractive Synthesis - One of the most common synth engine architectures, this is where waves with rich overtones, like sawtooth or square waves, are filtered and altered with envelopes to create sounds.
    
- Soundblaster(r) Live! - The successor to the AWE64, which improved the synthesiser chip to the EMU10K1, supporting modulators.
    
- Soundblaster(r) Audigy - The successor to the SB Live!, containing the EMU10K2 chip.
    
- Soundblaster(r) X-Fi - The successor to the SB Audigy, containing the EMU20K1 or EMU20K2 chip. Supports 24-Bit Soundfont(r) 2 files (2.04).
    
- Synth - Abbreviation of "Synthesiser", see "Synthesiser" in the 2.04 specification for more information.
    
- Version 3 - Refers to Werner SF3, a small upgrade to Soundfont(R) 2.04 created by Werner Schweer to allow an open source compression solution for SF programs (usually ogg, but can be any format).
    
- Version 4 - This new specification, based on Soundfont(r) 2.04 and Werner SF3, with a set of new features making it more realistic. Not to be confused with the unofficial Cognitone .sf4 file format, which is a variant of Werner SF3.
    

These changes:

- Articulation - Modulation of available parameters and usage of extra samples to produce expressive musical notes.
- Chorus - Effect which consists of cyclicly shifting pitches and mixing the results into themselves, resulting in a thicker sound. Version 4 adds types of chorus.
- Delay -
    - Meaning 1: Portion of a DAHDSR envelope before the amplitude changes to a non-zero value.
    - Meaning 2: An effect where a sample is repeated with the volume reducing until the sample is inaudible.
- Downloadable - SF version 2, 3 or SFe file obtained from the internet. (Old meaning referred to the obsolete ROM system)
- MIDI Bank - Groups of up to 128 presets, which can be selected by the two MIDI "Bank Select" control changes (CC00 and CC32).
- Reverb - An abbreviation for reverberation, this is an effect which applies stereo depth and a simulation of sampled instruments being played in different locations. Version 3 adds specific types of reverb.

And these removals:

- Preditor (refers to an old SF version 2 editor made by E-mu)

* * *

## 2.3 Parameter terminology

The parameter terminology used in version 4 is broadly the same as the E-mu(r) SF2.04 standard, with these additions:

- Amplification - An increase in volume or amplitude of a signal.
- Flat - Said of a tone that is lower in pitch than another reference tone.
- Round Robin - Samples switching one after another in a preset order. Usually done to improve realism.