# Section 6: "sdta-list" chunk

## 6.1 "smpl" sub-chunk

You can omit this sub-chunk if you provide ROM samples.

- This contains one or more samples of audio in linearly coded 16-bit, signed, little endian words.
- No more leeway of 46 zero-valued samples is required after each sample.
- Before saving, SFe editors should insert this leeway. Otherwise, they might give a warning telling the user that loop and interpolation quality may be affected.
- If ROM samples are detected in SFe files, attempt to load them, even if this sub-chunk is missing.
- If this sub-chunk is missing, and no ROM samples are found, show an error message as mentioned in the program specification.

* * *

## 6.1a About compression in SFe

To implement compression in your SFe bank, please use [Werner SF3](https://github.com/FluidSynth/fluidsynth/wiki/SoundFont3Format) compression encoding.

- Werner SF3 is widely used by the open source community.
- It is a standard that is being developed right now.
- There is no final specification, but the Fluidsynth team have a draft specification for Werner SF3.
- The goal is to make sure that these specifications are usable together.
- All SFe players must implement Werner SF3.
- Not all SFe files are required to implement Werner SF3 right now, but in the future it will become a requirement.
- Werner SF3 supports multiple different compression formats.
- The "scom" sub-chunk found in specification versions 4.00.3 and earlier is now obsolete.
- Incompatible SF compression formats (.sfark, .sfpack, .sf2pack, .sfq) are prohibited. You should use Werner SF3.

* * *

## 6.2 "sm24" and "sm32" sub-chunk

These sub-chunks are optional.

- The sm32 sub-chunk contains the least significant byte, and the sm24 sub-chunk contains the next least significant byte after sm32.
- Each sub-chunk is exactly half the size of the smpl sub-chunk.
- For every 2 bytes in the smpl sub-chunk, there is 1 byte in these sub-chunks.

![6.2a_1.png](../../../_resources/6.2a_1.png)

If these sub-chunks are present, they are combined with the other sub-chunks to create a sample with higher bitdepth.

- If the ifil version is below 2.04 (signifying an E-mu Systems(r) designed Soundfont(r) standard before 2.04), both sm24 and sm32 are ignored.
    
- If the ifil version is exactly 2.04 (signifying the E-mu Systems(r) designed Soundfont(r) 2.04 standard), only sm32 is ignored. The sm24 sub-chunk is still used.
    
- If these sub-chunks are not exactly half the size of the smpl sub-chunk (or otherwise invalid), the data should be ignored.
    
- If only the sm32 sub-chunk is invalid, the sm24 sub-chunk should still be loaded.
    
- However, if only the sm24 sub-chunk is invalid, both sub-chunks should be ignored.
    
- If the sm24 sub-chunk is ignored, the synthesiser should only attempt to render the first 16 bits of the samples contained within the smpl sub-chunk.
    
- If only the sm32 sub-chunk is ignored, the synthesiser should attempt to render both the smpl and sm24 sub-chunks, resulting in a 24-Bit sample.
    
- Due to the massive size, unpracticality and compatibility implications of 32-bit samples, use of the sm32 sub-chunk is not recommended! 
    

* * *

## 6.2a Using 8-bit samples

If the smpl sub-chunk is missing, but the sm24 or sm32 sub-chunks are present, 8-bit sample mode is to be activated.

- The sample depth is 8 bits.
- The length of the sm24 sub-chunk should be rounded up to the nearest byte, as if the sub-chunk was being used with an smpl sub-chunk.
- If somehow, you've got both an sm24 and an sm32 sub-chunk, but no smpl sub-chunk, the sm24 sub-chunk is the most significant byte, and 16-bit sample playback is assumed.
- Editing software should give a warning if there is an sm24 and an sm32 sub-chunk but no smpl sub-chunk, and should convert it to a 2.01-compliant 16-bit format.
- This mode is only enabled if all samples are 8-bit. You can not mix 8-bit and higher sample depths.
- Non-standard sample bit depths (6-bit, 12-bit, 18-bit, etc.) are not supported by SFe version 4.

* * *

## 6.3 Looping rules

- No more leeway of 8 samples is required.
- Before saving, SFe editors might give a warning about this leeway telling the user that loop and interpolation quality may be affected.