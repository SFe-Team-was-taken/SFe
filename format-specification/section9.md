# Section 9: Parameters and synthesis model

## 9.1 SF version 4 synthesis model

In version 4, the synthesis model has been massively improved compared to the EMU8000-based synthesis model of Soundfont(r) 2.04 and Werner SF3.

The model comprises of:

- A sample based oscillator.
- A dynamic low pass, high pass, band pass or notch filter with variable depth.
- An enveloping amplifier.
- Programmable sends to pan, reverb, chorus, compressor, delay, distortion, flanger, phaser and rotary effects.
- Round robin sample playback
- An underlying modulation engine includes:
    - Two LFOs
    - Two envelope generators.

* * *

## 9.1.1 Sample based oscillator

The method of operation is identical to SoundFont(R) 2.04.

* * *

## 9.1.2 Sample looping

- Playback of a digital sample by the sample based oscillator is described by:
    - A start point
    - An end point
    - One loop between two points.
    - In the future, SFe64 will have a method of describing an unlimited number of loop points.
- Samples can be flagged as looped or unlooped.
    - Unlooped samples will ignore any loop points.
    - Looped samples can be played in 5 different ways:
        - A normal loop - played from start to the loop point and loops, until the key is released.
        - Loop with release - played from start to the loop point and loops, however when the key is released, the rest of the sample plays back.
        - On release - played only when the key is released.
        - One shot - played from start to end without loop but does not fade out when key is released, only stops sounding at the end of the sample.
        - Bidirectional ("bidi") - played from start to end, reversing when it reaches the end, and reversing again when it reaches the start again, repeating until the key is released.
    - Additionally, the sample playback mode can be defined as either forward playback (as in SoundFont(R) 2.04) or reverse playback.

* * *

## 9.1.3 Filters

- The synthesis model consists of four types of filters:
    - A low-pass filter (as per SoundFont(R) 2.04)
    - A high-pass filter
    - A band-pass filter
    - A notch filter
- Each of the filters are idealised as shown in the SoundFont(R) 2.04 specification.
- The rolloff is configurable, but is by default 12dB/octave.
- \[Insert some figures of filter structures\]

* * *

## 9.1.4 Final gain amplifier

The method of operation is identical to SoundFont(R) 2.04.

* * *

## 9.1.5 Effects Sends

- In SFe64, this has been improved with a full set of DSP (digital signal processor) effects, which provide new effects all the way from distortion to rotary speaker.
- The pan system works in the same way as SoundFont(R) 2.04.
- Compared to SoundFont(R) 2.04, the chorus and reverb effects have been improved with different types of effects.
    - For example, the chorus send can be configured to instead add:
        - An additional flanger on top of the flanger provided
        - A celeste effect
        - A symphonic effect
        - An ensemble effect.
    - The reverb can be configured to simulate many different types of area, including:
        - A hall (small/medium/large)
        - A room (small/medium/large)
        - A stage
        - Plate reverb
        - A white room
        - A tunnel
        - A canyon
        - Gate reverb
        - Reverse gate reverb
        - Early reflections
        - A basement.

* * *

## 9.1.6 Low Frequency Oscillators (LFOs)

There are two LFOs which work in the same way as SoundFont(R) 2.04.

* * *

## 9.1.7 Envelope Generators

There are two envelope generators which work in the same way as SoundFont(R) 2.04.

* * *

## 9.1.8 Modulation interconnection

\[Insert figures of modulation interconnection\]

* * *

## 9.2 MIDI functions

Control Change #32 (Bank Select "LSB") has been modified to manipulate the high 8 bits of the wBank value.

All other MIDI functions are unchanged from SoundFont(R) 2.04.

If an SoundFont(R) 2.00a file is loaded, see the SoundFont(R) specification for more details for handling of SoundFont(R) 2.00 files.

* * *

## 9.3 Parameter units

All of these are the same as SoundFont(R) 2.04.

* * *

## 9.4 SF Generator Model

This is the same as SoundFont(R) 2.04.

* * *

## 9.5 SF Modulator Model

- When the Modulator Controller Source has been set to an Amplitude Based Source, amplitude is modulated instead of dBa.
- All other modulators work in the same way as SoundFont(R) 2.04.
- \[New diagrams available soon\]

* * *

## 9.6 NRPN implementation

The NRPN implementation used by version 4 is identical to previous versions of the format.

* * *