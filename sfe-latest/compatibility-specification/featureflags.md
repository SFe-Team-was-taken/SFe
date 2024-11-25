# SFe Feature Flags List 4.0.10

The feature flags system is split like this:

- Branches: Roughly corresponds to each version (but not all listed features are part of the version). Maximum of 256. Number may increase with later SFe64 wMajor versions.
- Leaves: Corresponds to each feature. Maximum of 256. These may change with later SFe64 wMajor versions. Contains 32-bit data declaring how much of the feature is implemented.
- Flags: Each of the 32-bits that comprise a leaf, declaring support for specific features.

## Branch 00: Foundational synthesis engine

### Leaf 00:00: Tuning

- Bit 1: Coarse tuning
- Bit 2: Fine tuning
- Bit 3: Root key

### Leaf 00:01: Looping

- Bit 1: Loop during release
- Bit 2: Non-loop during release

### Leaf 00:02: Filter Types

- Bit 1: Sound Blaster compatible low pass

### Leaf 00:03: Amplification and attenuation

- Bit 1: Attenuation supported in preset
- Bit 2: Attenuation supported in instrument
- Bit 3: Amplification supported in preset
- Bit 4: Amplification supported in instrument
- Bit 5: True dB supported. If not supported, 0.4x dB is supported.

### Leaf 00:04: Effects blocks

- Bit 1: Reverb supported
- Bit 2: Chorus supported
- Bit 3: Pan supported

### Leaf 00:05: Low Frequency Oscillators

- Bit 1: Vibrato supported
- Bit 2: Pitch Modulation
- Bit 3: Filter Modulation
- Bit 4: Amplitude Modulation

### Leaf 00:06: Envelopes

- Bit 1: Volume delay
- Bit 2: Volume attack
- Bit 3: Volume hold
- Bit 4: Volume decay
- Bit 5: Volume sustain
- Bit 6: Volume release
- Bit 7: Key to volume hold
- Bit 8: Key to volume decay
- Bit 9: Modulation delay
- Bit 10: Modulation attack
- Bit 11: Modulation hold
- Bit 12: Modulation decay
- Bit 13: Modulation sustain
- Bit 14: Modulation release
- Bit 15: Key to modulation hold
- Bit 16: Key to modulation decay
- Bit 17: Modulation of pitch
- Bit 18: Modulation of filter

### Leaf 00:07: MIDI Control Changes

- Bit 1: 00 Bank Select MSB
- Bit 2: 06 Data Entry MSB
- Bit 3: 32 Bank Select LSB (Multiple banks)
- Bit 4: 38 Data Entry LSB
- Bit 5: 64 Sustain
- Bit 6: 66 Soft
- Bit 7: 67 Sostenuto
- Bit 8: 98 NRPN LSB
- Bit 9: 99 NRPN MSB
- Bit 10: 100 RPN LSB
- Bit 11: 101 RPN MSB
- Bit 12: 120 All sound off
- Bit 13: 121 Reset all controllers
- Bit 14: 123 All notes off
- Bit 15: 32 Bank Select LSB (wBank support)
- Bit 16: Sysex changes with wPreset (4.3 and later)

### Leaf 00:08: Generators

- Bit 1: Index gen support
- Bit 2: Range gen support
- Bit 3: Substitution gen support
- Bit 4: Sample gen support
- Bit 5: Value gen support
- Bit 6: PGEN support
- Bit 7: IGEN support

### Leaf 00:09: Zones

- Bit 1: Key range
- Bit 2: Velocity range
- Bit 3: Exclusive class
- Bit 4: Fixed key
- Bit 5: Fixed velocity
- Bit 6: Sample offset
- Bit 7: Loop offset

### Leaf 00:0a: SFCF support (4.2 and later)

- Bit 1: Always play sample to end
- Bit 2: DLS vel-to-vol env.atk
- Bit 3: DLS vel-to-mod env.atk
- Bit 4: Vibrato LFO to volume

## Branch 01: Modulators and NRPN

### Leaf 01:00: Modulators

- Bit 1: Primary source
- Bit 2: Secondary source
- Bit 3: Transform support
- Bit 4: Linear curves
- Bit 5: Concave curves
- Bit 6: Convex curves
- Bit 7: Switch curves
- Bit 8: Positive unipolar
- Bit 9: Negative unipolar
- Bit 10: Positive bipolar
- Bit 11: Negative bipolar
- Bit 12: Modulator chaining
- Bit 13: PMOD support
- Bit 14: IMOD support

### Leaf 01:01: NRPN

- Bit 1: NRPN select MSB=120
- Bit 2: NRPN select LSB: 1-2 digits
- Bit 3: NRPN select LSB: 3 digits
- Bit 4: NRPN select LSB: 4 digits
- Bit 5: NRPN select LSB: 5 digits

### Leaf 01:02: DMOD chunk (4.1 and later)

- Bit 1 off, bit 2 off: No support
- Bit 1 on, bit 2 off: Read support only
- Bit 1 on, bit 2 on: Playback support

### Leaf 01:03: PNMM chunk (4.1 and later)

- Bit 1 off, bit 2 off: No support
- Bit 1 on, bit 2 off: Read support only
- Bit 1 on, bit 2 on: Playback support
- Bit 3: NRPN
- Bit 4: RPN
- Bit 5: MSB
- Bit 6: LSB

## Branch 02: Sample bitdepth support

### Leaf 02:00: 24-bit support

- Bit 1 off, bit 2 off: No support
- Bit 1 on, bit 2 off: Read support only
- Bit 1 on, bit 2 on: Playback support
- Bit 3: 8-bit support

### Leaf 02:01: 32-bit support

- Bit 1 off, bit 2 off: No support
- Bit 1 on, bit 2 off: Read support only
- Bit 1 on, bit 2 on: Playback support
- Bit 2: Support for combining two 8-bit chunks into a 16-bit sample

## Branch 03: Compression support (WernerSF3)

### Leaf 03:00: Compression flag

- 0: sfSampleType bit 4 unsupported
- 1: sfSampleType bit 4 supported

### Leaf 03:01: Sample compression formats

- Bit 1: OGG
- Bit 2: Opus
- Bit 3: FLAC
- Bit 4: MP3

## Branch 04: Metadata upgrades

### Leaf 04:00: Metadata improvements

- Bit 1: UTF-8 in INFO
- Bit 2: UTF-8 in pdta

### Leaf 04:01: Preset management system

- Bit 1: dwLibrary support (4.4 and later)
- Bit 2: dwGenre support (4.4 and later)
- Bit 3: dwMorphology support (future version)
