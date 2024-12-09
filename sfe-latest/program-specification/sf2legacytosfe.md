# SF2 to SFe converter program specification 4.0.11

## A legacy SF2.04 to SFe converter may be constructed in many different ways.

SFe files are very similar in structure to legacy SF2.04 files, with these important differences:

- `ifil` version is updated from `2.04` to `2.1024`
- `isng` is updated to `SFe 4`
- `sm32` and `scom` sub-chunks are added
- Unused `wPreset` and `wBank` bits are used
- New `SFModulator` enum options
- Default modulators 1-4 are removed
- SFe ROM emulator support
- `ISFe-list` subchunk in `INFO-list` chunk contains SFe-specific information

### Conversion from legacy SF2.04 to SFe:

- Upgrade the `ifil` version in the header from `wMajor=2`, `wMinor=4` to `wMajor=2`, `wMinor=1024`.
- Overwrite the `isng` value with `SFe 4`.
- Create an `ISFe-list` subchunk with information: `SFty = "SFe-static"`, `SFvx = 4, 0, Milestone, 11, "4.0.11"`, `flag` corresponding to features used in the bank.
- Add modulators to instruments that replace the default modulators 1-4, if used.
- Remove modulators that override the default modulators 1-4.

### Conversion from SFe to legacy SF2.04:

- Downgrade the `ifil` version in the header from `wMajor=2`, `wMinor=128` to `wMajor=2`, `wMinor=4`.
- Overwrite the `isng` value with `X-Fi`.
- Decompress the samples if the bank uses SFe Compression.
- Downsample any 32-bit samples to 24-bit, and remove the `sm32` sub-chunk.
- Convert all 8-bit samples to 16-bit by moving the sample data to the `smpl` sub-chunk.
- If the first 8 bits of either `wPreset` or `wBank` are identical to another patch, keep only the patch with bits 9-16 clear. If this is not found, keep only the last of the patches in the record. Clear bits 9-16 of all patches afterwards.
- Remove all modulators that implement default modulators 1-4.
- Add modulators that override the default modulators 1-4.
- Remove the `ISFe-list` subchunk.

### Conversion from SFe to legacy SF2.01:

- Downgrade the `ifil` version in the header from `wMajor=2`, `wMinor=128` to `wMajor=2`, `wMinor=1`.
- Overwrite the `isng` value with `EMU8000` or `E-mu 10K1`.
- Decompress the samples if the bank uses SFe Compression.
- Downsample any 24-bit or 32-bit samples to 16-bit, and remove the `sm24` and `sm32` sub-chunks.
- Convert all 8-bit samples to 16-bit by moving the sample data to the `smpl` sub-chunk.
- If the first 8 bits of either `wPreset` or `wBank` are identical to another patch, keep only the patch with bits 9-16 clear. If this is not found, keep only the last of the patches in the record. Clear bits 9-16 of all patches afterwards.
- Remove all modulators that implement default modulators 1-4.
- Add modulators that override the default modulators 1-4.
- Remove the `ISFe-list` subchunk.