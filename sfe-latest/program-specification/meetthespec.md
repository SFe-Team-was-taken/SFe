# What happens if the specification is not met?

### File Size Representation

- SFe is a 32-bit or 64-bit format.
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
- Werner SF3 support is required; the SFe format incorporates Werner SF3 structures (SFe Compression).
- Programs that cannot recognise Werner SF3 format (SFe Compression) may not be able to open SFe files.
- 24-bit support is optional, but if 24-bit is unsupported in an SFe player, legacy SF2.04 files must not be rejected.
- Backward compatibility with legacy SF2.0x is sacrosanct when using 32-bit chunk headers, take care when creating a program.
- "Synthfont Custom Features" support is not currently included in the specification.

### Header Support

- The header should be "RIFF" and "sfbk" with 32-bit chunk headers to preserve legacy SF2.0x compatibility.
- 32-bit only programs should recognise 64-bit chunk headers and give an error.
- The header should be "BW64"/"RF64" and "sfen" with 64-bit chunk headers.
- All programs that support 64-bit chunk headeres must also support 32-bit chunk headers.

### Sample Compression

- Compression algorithms vary, but we recommend at least one of each lossy and lossless algorithms.
- OGG and FLAC are specified in the specification.
- Werner SF3 was designed to use OGG files, so OGG is a good start for lossy algorithms.
- Opus is an alternative that is "better" than OGG according to some people.
- FLAC and "Wavpack" are free lossless compression algorithms for sounds.
- Note that while "Wavpack" has advantages over FLAC, it is not widely supported.

### File Extension, Structure, Information and Metadata

- The file extension is .sft. Chunk headers must be detected.
- Do not save SFe files with an extension .SF2, as it may confuse legacy SF2.0x players.
- Use the ifil and SFvx subchunks to determine version, do not use the file extension.
- For SFe, you must use the prescribed chunk sizes and limits in the specification.

### Sample Specifications

- SFe requires 96kHz frequency, because it is the next standard frequency above 50kHz as specified by SF2.04.
- 88.2kHz is not recommended because it is non-standard.
- Stray sdta sub-chunks must be ignored. Erroring out on extra sdta chunks is not compliant with SF2.04.
- There must not be additional limitations to sample length, besides the file size limits.
- Sample linking features from legacy SF2.04 must be supported (with the exception of SFe Compression).

### Instrument Specifications

- High numbers of samples per instrument are specified to ensure that the program works efficiently.
- Ideally, programs should support unlimited numbers of samples per instrument.
- You must not add restrictions to number of samples per instrument or simultaneous samples.
- Modulators are fixed and must be implemented as shown in the specification and not as in SF2.04.
- In legacy SF2.04 compatibility mode, bug compatibility can be implemented.
- When field sizes increase from 20 characters, programs should be able to display at least 64 characters.
- If it is not possible to display the entire field, use an ellipsis or similar.

### Player Specifications

- A minimum polyphony of 256 notes is in place if possible.
- The byBankLSB percussion toggle is to fix the bank select LSB function.
- All control changes listed as "mandatory" in the SFe specification must be supported.
- If it is not supported, playback may be severely impacted, resulting in a program that is not SFe compliant.
- This is already a problem with legacy SF2.0x, as not all SF2 players support modulators.
- Reset support and multiple simultaneous drum kits might not be required, but it is suggested.
- 64-channel MIDI file support is suggested, and may be required in the future for SFe.
- The ROM emulator may be required in the future, as many SFe files will make full use of it.