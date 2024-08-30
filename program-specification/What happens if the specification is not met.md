# What happens if the specification is not met?

### File Size Representation

- The number of bits is represented in the file format name (SFe32 and SFe64).
- Incorrect numbers of bits will therefore result in program non-compliance.
- Signed integers are not useful because a negative file size is impossible.
- To ensure that file size limits are not arbitrarily "cut in half", signed integers are prohibited.
- Programs using signed integers to represent file size are therefore not compliant with SFe.

### File Size Limit

- You should not impose additional file size limits in SFe programs.
- SFe files that exceed these limits may not play.
- Because compatibility is not guaranteed, such programs may not be SFe compliant.

### Sample Streaming

- You should strive to include disk streaming support.
- This is because the file size limit is almost always greater than the system memory installed.
- System memory streaming options may be available for higher performance.

### Total File Size Limit and Multiple Files

- Always provide space for more than one file.
- SFe allows flexibility in implementing multiple files.
- It will be standardised in the future depending on the most popular system.
- The program specification requires multiple files, to guarantee proper operation of "split bank" files.
- Not implementing multiple file operation will affect compatibility.
- Such programs therefore may not be SFe compliant.

### Legacy Support

- SFe is designed to reconcile incompatible SF extensions.
- Werner SF3 support is required; the SFe format incorporates Werner SF3 structures.
- Programs that cannot recognise Werner SF3 format may not be able to open SFe files.
- For SFe64, 24-bit support (SF 2.04) is mandatory, while for SFe32, it is optional.
- If 24-bit is unsupported in an SFe32 player, SF 2.04 files must not be rejected.
- Backward compatibility with SF 2.0x in SFe32 is sacrosanct, take care when creating a program.
- "Synthfont Custom Features" support is optional - this is not included in the specification.
- If we get permission from the Synthfont author, we can incorporate it into SFe at a later date.

### Header Support

- The header should be "RIFF" in SFe32 to preserve SF 2.0x compatibility.
- SFe32 only programs should recognise 64-bit headers and give an error.
- 64-bit headers used by SFe64 are "BW64" and "RF64".

### Sample Compression

- Compression algorithms vary, but we recommend at least one of each lossy and lossless algorithms.
- OGG and FLAC are specified in the specification.
- Werner SF3 was designed to use OGG files, so OGG is a good start for lossy algorithms.
- Opus is an alternative that is "better" than OGG according to some people.
- FLAC and "Wavpack" are free lossless compression algorithms for sounds.
- Note that while "Wavpack" has advantages over FLAC, it is not widely supported.

### File Extension, Structure, Information and Metadata

- The file extensions are .SFe32 and .SFe64.
- Alternatively, .SFe can be used and the header used to detect 32 or 64-bit mode.
- Do not save SFe files with an extension .SF2, as it may confuse SF2.0x players.
- Use the ifil subchunk to determine version, do not use the file extension.
- For SFe32, deviation from the prescribed chunk sizes and limits by E-mu will result in incompatibilities.
- Any incompatibility with SF2.04 files will result in the implementation being non-compliant.
- For SFe64, you must use the prescribed chunk sizes and limits in the specification.
- Switch between the structures when detecting 32 or 64-bit mode.
- All SFe64 players must also be able to play SFe32 files.

### Sample Specifications

- The E-mu specification specifies 50kHz frequency and 16-bit sample depth.
- SFe32 implementations must achieve at least that to ensure compatibility with SF2.0x.
- Failure to do so can result in reduced sound quality, samples being off-pitch, or other serious sound issues.
- SFe64 requires 96kHz frequency, because it's the next standard frequency above 50kHz.
- 88.2kHz is not recommended because it is non-standard.
- As specified before, SFe64 implementations require 16 and 24-bit support.
- If this is absolutely not possible, stray sdta sub-chunks must be ignored.
- Do not error out on extra sdta chunks, as this may not be compliant with SF2.04.
- There must not be additional limitations to sample length, besides the file size limits.
- Sample linking features from SF2.04 must be supported.
- For SFe64, basic surround sample support using the "link" mode is required.
- Full surround decoding is not required, but programs must gracefully fallback to stereo.

### Instrument Specifications

- High numbers of samples per instrument are specified to ensure that the program works efficiently.
- Ideally, programs should support unlimited numbers of samples per instrument.
- You must not add restrictions to number of samples per instrument or simultaneous samples.
- Modulators are fixed and must be implemented as shown in the specification and not as in SF2.04.
- In SF2.04 compatibility mode, bug compatibility can be implemented.
- Extra enumerators are only for SFe64, and have not been implemented yet.
- When field sizes increase from 20 characters, programs should be able to display at least 64 characters.
- If it is not possible to display the entire field, use an ellipsis or similar.

### Player Specifications

- A minimum polyphony of 256 notes is in place if possible.
- The second percussion toggle is to fix the wBank implementation of bank select CC32.
- All control changes listed as "mandatory" in the SFe specifications must be supported.
- If it is not supported, playback may be severely impacted, resulting in a program that is not SFe compliant.
- This is already a problem with SF2.01 and later versions, as not all SF2 players support modulators.
- Reset support and multiple simultaneous drum kits might not be required, but it is suggested.
- 64-channel MIDI file support is suggested for SFe32, and will be required in the future for SFe64.
- The ROM emulator is required as many SFe files will make full use of it.