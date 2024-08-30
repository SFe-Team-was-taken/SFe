# Section 8: Enumerators

## 8.1.1 Kinds of generator enums

\[I'm going to do this later.\]

* * *

## 8.1.2/3 Generator enums definitions

SFe64 will extend the Generator system to allow 127 different types of Generators.

The Generator Enums used in SFe 4.00, are broadly the same as the SoundFont(R) 2.04 standard, with these additions:

- Generator #14: Round Robin Sample Playback Class (rrSamplePlaybackClass)
    
    - Defined as a DWORD (32-Bit Unsigned Value).
    - This allows samples to be played sequentially ("round-robin" sample playback).
    - Assume that 5 samples are defined in an instrument, one with a Generator #14 value of 1 to 5.
    - When the sample division is first triggered, the sample with a Generator #14 value of 1 is played back.
    - After this, when the sample division is triggered again, the sample with a Generator #14 value of 2 is played back.
    - This repeats until the sample with the highest number in this division is played.
    - When the last sample has played, which in this case is the sample with a Generator #14 value of 5, the next keypress will result in the playback of the sample with a Generator #14 value of 1.
    - Multiple samples can be triggered at the same time if they have identical Generator #14 values.
    - A value of zero means that no round-robin sample playback will occur.
- Generator #18: Filter Type (filterType)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - This allows users to use different types of filters.
    - Defined Values:
        - Zero - Low pass filter
        - 1 - High pass filter
        - 2 - Band pass filter
        - 3 - Notch filter
        - 4 to 7 - Formant filters 1 to 4
        - 127 - No filter
    - The default value is zero.
    - If the value is not between zero and 7, the default value of zero should be assumed, and therefore a low pass filter should be activated.
    - More filters will be defined in the future.
    - Reference implementation of formant filters will come in the future.
- Generator #19: Filter Depth (filterDepth)
    
    - Defined as a CHAR (8-bit value) - it was a LONG in 4.00.1.
    - This allows users to change the depth of the filter.
    - The default value is "12".
    - Zero filter depth is invalid. If the value is zero, the default value of "12" should be assumed.
- Generator #20: Modulation LFO Type (modLfoType)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - Defined Values:
        - Zero - Sine
        - 1 - Triangle
        - 2 - Ramp up
        - 3 - Ramp down
        - 4 - Sample and Hold
        - 5 - Square
    - More types will be defined in the future.
- Generator #42: Conditional Start Condition (conditionalStartCondition)
    
    - Defined as a LONG (32-bit value)
    - Defined Values:
        - Zero - On key press
            
            - No conditional start condition is applied, the sample will play every time its division is triggered.
        - 2 to 120 (excluding values referring to invalid control changes) - On MIDI controller value (key press required).
            
            - 2 corresponds to CC#1 (modulation wheel), 120 corresponds to CC#119, etc.
            - An example of usage is switching the sample at the time where the key will be pressed if the modulation wheel value is set to 127.
            - It is possible to do this with this mode, to do this add:
                - Generator #42 = 2 (corresponding to CC#1 (the modulation wheel) and the condition being "Equal to").
                - Generator #49 = 127
            - This should be added to the separate sample to be played back at CC#1 = 127. On the other sample played back at CC#1 = zero to 126, add:
                - Generator #42 = 1026 (corresponding to CC#1 (the modulation wheel) and the condition being "Not Equal to").
                - Generator #49 = 127
            - 128 - On pitch bend value (key press required).
                - It will trigger if the pitch bend value is above or below a set amount.
            - 256 - First key, if the key is the first key pressed, playback the sample.
                - On drawbar organs, only the first note would play the "percussion" sound. This mode is good for emulating this.
                - In order to do that, sample the organ percussion separately and add:
                    - Generator #42 = 256 (to activate first key mode).
                    - Generator #49 = 1 (optional, as the default value of Generator #49 when Generator #42 = 256 is 1)
            - 384 - Legato, other keys must be pressed before playback of the sample.
                - Good for applying a realistic transition (a type of articulation) between notes in solo instruments which can only play one note at a time.
                - For example, it is possible to add:
                    - Generator #42 = 384 (to activate legato mode).
                    - Generator #49 = 1 (optional, as the default value of Generator #49 when Generator #42 = 384 is 1)
                - In this case, if the instrument is playing polyphonically (assuming that no exclusive classes are defined), the sample will not playback.
                - Modifying the value of Generator #42 to 4380 will change the condition to permit the sample to playback even if more than 1 note is sounding at the same time.
                - No portamento will be added by this Generator.
                - In order to adjust portamento, another Generator related to the exclusive class will do so.
            - 514 to 632 - (excluding values referring to invalid control changes) On MIDI controller value (key press not required).
                - 514 corresponds to CC#1 (modulation wheel), 632 corresponds to CC#119, etc.
                - Example: If these generators are set:
                    - Generator #42 = 4673 (corresponding to CC#64 (the sustain pedal) and the condition "Above or Equal to")
                    - Generator #49 = 64 (corresponding to the sustain pedal value being 64)
                - The sample would playback every time the CC#64 is brought to at least 64.
                - It would playback once and the sound would stop (assuming that loops are not activated).
                - It would not playback until the CC#64 is brought below 64 and brought back up to at least 64.
                - Loops will still apply. If there is no decay defined for the sample, it would playback continuously until the CC#64 is below 64.
                - Once the conditional start condition no longer applies, playback will stop, with the volume envelope release time set on the Instrument or Preset Generator.
                - This specific scenario is good for emulating the pedal sound on a piano.
                - By putting these generators on the pedal down sample, the sample will playback when you push down the sustain pedal.
                - Another set of generators can be used on the pedal up sample. For example:
                    - Generator #42 = 3137 (corresponding to CC#64 (the sustain pedal) and the condition "Below")
                    - Generator #49 = 64 (corresponding to the sustain pedal value being 64)
                - When the sustain pedal is released, the pedal up sample will playback.
            - 640 - On pitch bend value (key press not required).
                - The sample would playback every time the conditional start condition applies.
                - It would playback once and the sound would stop (assuming that loops are not activated).
                - It would not playback until the conditional start condition no longer applies, and then the conditional start condition applies once again.
                - Loops will still apply. If there is no decay defined for the sample, it would playback continuously until the conditional start condition no longer applies.
                - Once the conditional start condition no longer applies, playback will stop, with the volume envelope release time set on the Instrument or Preset Generator.
            - 770 to 888 (excluding values referring to invalid control changes) - On MIDI controller value (key hold or key press required).
                - Note: If the sample triggered by the Control Change ends before the Control Change is moved back to its original position, the note will not continue to sound, it is necessary for the note to be retriggered again.
                - However, if the Control Change moves back to a position where it does not satisfy the conditional start before the Control Change triggered sample ends, the original sample will keep on playing.
            - 896 - On pitch bend value (key hold or key press required).
                - This mode would be good for programming trumpet/trombone falls.
                - For example:
                    - Generator #42 = 3968 (To set the condition to "Below")
                    - Generator #49 = -20000 (corresponding to the pitch bend value being below -20000)
                - Note: If the sample triggered by the pitch bend wheel ends before the pitch bend wheel is moved back to its original position, the note will not continue to sound, it is necessary for the note to be retriggered again.
                - However, if the pitch bend wheel moves back to its original position before the pitch bend wheel trigger sample ends, the original sample will keep on playing.
        - To change the condition of comparing a value, add these amounts:
            
            - Add Zero - Equal to
            - Add 1024 - Not Equal to
            - Add 2048 - Above
            - Add 3072 - Below
            - Add 4096 - Above or Equal to
            - Add 5120 - Below or Equal to
        - The default value is zero.
            
        - Later versions of the draft specification will have more conditional start conditions, like key switching. They will also make this clearer by assigning different actions to different bits of this value.
            
- Generator #48: Initial Attenuation (initialAttenuation)
    
    - Redefined to a signed value (SFe64)
        - Defined Values: -1440 to 1440 (SFe64).
    - Negative attenuation is now possible.
    - Therefore, the instrument can be made louder.
- Generator #49: Conditional Start Value
    
    - Defined Values: -32768 to 32767 (Zero to 127 for MIDI Control Changes)
        - This is the value of the MIDI controller which a conditional start condition is based on.
- Generator #54: Sample Looping Modes (sampleModes)
    
    - This generator is already defined in SoundFont(R) 2.04, but now it is updated with new looping modes. (SFe64)
    - Now there are eight bit flags instead of two.
    - Defined Values:
        - Zero - No loop
        - 1 - Normal loop
        - 2 - No loop
        - 3 - Loop, playing rest of the sample on keyoff
        - 4 - Release
        - 5 - One Shot
        - 6 - Bidirectional (bidi/back and forth)
        - 128 - No loop (reverse)
        - 129 - Normal loop (reverse)
        - 130 - No loop (reverse)
        - 131 - Loop, playing rest of the sample on keyoff (reverse)
        - 132 - Release (reverse)
        - 133 - One Shot (reverse)
        - 134 - Bidirectional (reverse)
    - Adding 128 to a value will reverse the sample playback.
- Generator #55: Exclusive Class Mode (exclusiveClassMode)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - Defined Values:
        - Zero - Abrupt release, no retrigger (same as in SoundFont(R) 2.04)
        - 1 - Abrupt release, retrigger.
            - If the original key is still held, but a second key has been pressed and released, retrigger means that the first key will sound again.
        - 2 - Gradual release, no retrigger, no portamento.
            - The time taken for the old note to transition to the new note is equal to the value specified in the Volume Envelope Release Generator.
        - 3 - Gradual release, retrigger, no portamento.
            - Same as if the value is 2, but the retrigger mechanism of value 1 is enabled.
        - 6 - Gradual release, no retrigger, portamento.
            - The time taken for the old note to transition to the new note (including portamento (a smooth transition in pitch between notes) is equal to the value specified in the Volume Envelope Release Generator.
        - 7 - Gradual release, retrigger, portamento.
            - Same as if the value is 6, but the retrigger mechanism in both values 1 and 3 is enabled.
    - The default value is zero.
- Generator #59: Vibrato LFO Type (vibLfoType)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - Defined Values:
        - Zero - Sine
        - 1 - Triangle
        - 2 - Ramp up
        - 3 - Ramp down
        - 4 - Sample and Hold
        - 5 - Square
    - The default value is zero.
- **Generator #60: Reserved (reserved4) (SFe64)**
    
    - **Generator #60 is no longer the final generator available in SFe64.**
- Generator #65: Compressor Threshold (compressorThreshold) (SFe64)
    
    - Defined Values: -1440 to zero. (-144db to zero db)
- Generator #66: Compressor Ratio (compressorRatio) (SFe64)
    
    - Defined Values: 10 to 1000 (1:1 to 100:1)
- Generator #67: Compressor Attack (compressorAttack) (SFe64)
    
    - Defined Values: -12000 to 8000 (Like Generator #34, 1 ms to 100 sec)
- Generator #73: Delay Time (delayTime) (SFe64)
    
    - Defined Values:
        - If Generator #74 (delaySync) = Zero
            - \-12000 to 8000 (Like Generator #34, 1 ms to 100 sec)
        - If Generator #74 (delaySync) = 1
            - \-3 - Every semibreve (1 Beats)
            - \-2 - Every minim (1/2 Beat)
            - \-1 - Every crotchet (1/4 Beat)
            - Zero - Every quaver (1/8 Beat)
            - 1 - Every semiquaver (1/16 Beat)
            - 2 - Every demisemiquaver (1/32 Beat)
            - And so forth, up to 63.
            - Add 64 for dotted notes.
                - For example, dotted semiquavers would be 65.
            - Add 128 for triplets.
                - For example, demisemiquaver triplets would be 130.
- Generator #74: Delay Sync (delaySync) (SFe64)
    
    - Defined Values:
        - Zero - Not synced to tempo
        - 1 - Synced to tempo
- Generator #75: Delay Feedback (delayFeedBack) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (zero percent to 100 percent)
- Generator #76: Reserved (reserved5) (SFe64)
    
- Generator #81: Distortion Effect Send (distEffectsSend) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (Zero percent to 100 percent)
- Generator #82: Distortion Effect Type (distEffectsType) (SFe64)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - Defined Values:
        - Zero: distortion
        - 1: overdrive
    - More will be added soon.
- Generator #89: Flanger Effect Send (flangerEffectsSend) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (Zero percent to 100 percent)
- Generator #90: Flanger Depth (flangerEffectsDepth) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (Zero percent to 100 percent)
- Generator #91: Flanger Feedback (flangerEffectsFeedBack) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (Zero percent to 100 percent)
- Generator #97: Phaser Effect Send (phaserEffectsSend) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (Zero percent to 100 percent)
- Generator #98: Phaser Depth (phaserEffectsDepth) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (Zero percent to 100 percent)
- Generator #99: Phaser Stage Count (phaserEffectsStageCount) (SFe64)
    
    - Defined Values:
        - Zero to 15 (zero to 15 stage)
- Generator #100: Phaser Feedback (phaserEffectsFeedBack) (SFe64)
    
    - Defined Values:
        - Zero to 1000 (Zero percent to 100 percent)
- Generator #105: Rotary Speaker Type (rotaryEffectsType) (SFe64)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - Defined Values:
        - Zero - No rotary speaker
        - 1 - Rotary speaker
    - More may be added soon.
- Generator #106: Rotary Speaker Speed Select (rotaryEffectsSpeed) (SFe64)
    
    - Defined Values:
        - \-16000 to 4500 (0.001Hz to 100Hz)
- Generator #107: Rotary Speaker Slow Speed (rotaryEffectsSlowSpeed) (SFe64)
    
    - Defined Values:
        - \-16000 to 4500 (0.001Hz to 100Hz)
    - Default Value: \[tbd\]
- Generator #108: Rotary Speaker Fast Speed (rotaryEffectsFastSpeed) (SFe64)
    
    - Defined Values:
        - \-16000 to 4500 (0.001Hz to 100Hz)
    - Default Value: \[tbd\]
- Generator #113: Reverb Type (reverbEffectsType) (SFe64)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - Defined Values:
        - Zero to 7 - Hall 1 to 8
        - 8 to 15 - Room 1 to 8
        - 16 to 23 - Stage 1 to 8
        - 24 to 31 - Plate 1 to 8
        - 32 to 35 - Early Reflections 1 to 4
        - 36 to 40 - Gate Reverb 1 to 4
        - 31 to 44 - Reverse Gate Reverb 1 to 4
        - 45 to 46 - White Room 1 and 2
        - 47 to 48 - Tunnel 1 and 2
        - 49 to 50 - Canyon 1 and 2
        - 51 to 52 - Basement 1 and 2
        - 64 to 65 - Hall Small 1 and 2
        - 66 to 67 - Hall Medium 1 and 2
        - 68 to 69 - Hall Large 1 and 2
        - 70 to 71 - Room Small 1 and 2
        - 72 to 73 - Room Medium 1 and 2
        - 74 to 75 - Room Large 1 and 2
    - More will be added soon.
- Generator #114: Chorus Type (chorusEffectsType) (SFe64)
    
    - Defined as a CHAR (8-bit value) - it was an unsigned CHAR in 4.00.1.
    - Defined Values:
        - Zero to 15 - Chorus 1 to 16
        - 16 to 23 - Celeste 1 to 8
        - 24 to 31 - Flanger 1 to 8
        - 32 to 39 - Symphony 1 to 8
        - 40 to 47 - Ensemble 1 to 8
        - 64 to 67 - Chorus 17 to 20
        - 68 to 71 - Feedback Chorus 1 to 4
        - 72 to 75 - Flanger 9 to 12
    - More will be added soon.
- Generator #127: End of Defined List (endOper) (SFe64)
    

* * *

## 8.2.1 Source enum controller palettes

\[This will be added soon. How did I forget about this?\]

* * *

## 8.2.2-3 Source Directions and Polarities

These are identical to SoundFont(R) 2.04.

* * *

## 8.2.4 Source Types

In SoundFont(R) 2.04, there are 4 sources.

This means that using the modulation wheel to crossfade between samples is possible.

- This means that using the modulation wheel to crossfade between samples is possible.
    
    - However, when the modulation wheel is equal to 64 (the centre), the output is quieter than when the modulation wheel is equal to zero or 127.
    - Therefore, there is a need to introduce new source types to solve the issue.
- The controller source types from zero to 3 are now considered dBa based. (SFe64)
    
    - This means that the equations used to apply all the source types are based on decibels instead of amplitude.
    - Since the decibel scale is logarithmic, adding together two sources with an opposite direction does not result in constant volume.
    - In the 32-bit format, controller source types zero to 3 remain amplitude based.
- New Source Types (SFe64)
    
    - These are only defined for SFe64. Usage with SFe32 or legacy SF players that were created to the SF2.04 specification will result in a loss of modulator playback.
        
    - SFe64, version 4 compatible players should accept these values in an SFe32 file anyway, if the SF version is 2.128 or above.
        
    - Controller Source Type #4: dBa Based Gradual Switch
        
        - This is like the Controller Source Type #3, with an important difference:
            - Unlike Controller Source Type #3, which switches abruptly at the value of the modulator being 64, this switches gradually.
            - The time taken for this gradual switch is equal to the volume envelope release time defined in the igen Sub-chunk and the pgen Sub-chunk.
            - The gradual switch is linear, and applied to the dBa value of the sample.
- Controller Source Type #16: Amplitude Based Linear
    
    - This is the same as the Controller Source Type #0, except instead of being based on the decibel scale, this is based on the amplitude scale.
    - The amplitude scale is a linear scale instead of a logarithmic scale.
    - Therefore, when crossfading two samples, the amplitude will remain constant.
- Controller Source Type #17: Amplitude Based Concave
    
    - This is the same as the Controller Source Type #1, except instead of being based on the decibel scale, this is based on the amplitude scale.
    - The amplitude scale is a linear scale instead of a logarithmic scale.
    - The mathematical equation defined by SoundFont(R) 2.04 is applied to the amplitude instead of the dBa value of the sample.
    - This mathematical equation is "Log(Sqrt(Value^2)/(MaxValue^2))" (same as SoundFont(R) 2.04).
- Controller Source Type #18: Amplitude Based Convex
    
    - This is the same as the Controller Source Type #2, except instead of being based on the decibel scale, this is based on the amplitude scale.
    - The amplitude scale is a linear scale instead of a logarithmic scale.
    - The mathematical equation defined by SF2.04 is applied to the amplitude instead of the dBa value of the sample.
    - This mathematical equation is the same as Controller Source Type #17, but is reversed (same as SF2.04).
- Controller Source Type #20: Amplitude Based Gradual Switch
    
    - This is the same as the Controller Source Type #4, except instead of being based on the decibel scale, this is based on the amplitude scale.
    - The amplitude scale is a linear scale instead of a logarithmic scale.
    - The gradual switch is applied to the amplitude instead of the dBa value of the sample.
- In general, adding 16 to the value of the Controller Source Type will switch the Controller Source from dBa based to Amplitude based.
    
    - Be careful, as this does not apply for the "Switch" Controller Source Type (Controller Source Type #3).
    - The Controller Source Type #16-#20 only has a difference between the Controller Source Type #0-#4 when attenuation or any other volume-related Generator is selected as the destination of the modulator.
    - Otherwise, it acts identically to the Controller Source Type #0-#4.

* * *

## 8.3 Modulator transform enums

These are identical to SoundFont(R) 2.04.

* * *

## 8.4.1-4 Default modulators 1-4

These have been removed, and no longer exist.

* * *

## 8.4.5-10 Default modulators 5-10

These are identical to SoundFont(R) 2.04.

* * *

## 8.5 Precedence, Absolute/Relative Values and Preset Level Availability of Generators.

The rules for precedence and absolute/relative values are identical to SoundFont(R) 2.04.

All new Generators introduced in version 4 (except for Conditional Start) are available in both the Instrument Level and the Preset Level.