# SFe file repair program specification

## Version 4.00.8

This specification has been written to provide a guideline for how SFe banks can be repaired by a program. This specification is applicable for legacy SF 2.04, Werner SF3 and SFe.

## 0.1 Revision history

|     |     |     |
| --- | --- | --- |
| Revision | Date | Description |
| 4.00.8 | October 30, 2024 | Initial release |

## 0.2 Specification versioning

The file repair program specifications follow the SFe versions.

## 0.3 Updates and comments

Please contact the SFe Team using the links found in the SFe specification.

## 0.4 Table of contents

- [SFe file repair program specification](#sfe-file-repair-program-specification)
    - [0.1 Revision history](#01-revision-history)
    - [0.2 Specification versioning](#02-specification-versioning)
    - [0.3 Updates and comments](#03-updates-and-comments)
    - [0.4 Table of contents](#04-table-of-contents)
- [Section 1: Introduction](#section-1-introduction)
    - [1.1 Scope and purpose of this document](#11-scope-and-purpose-of-this-document)
    - [1.2 Improvements and enhancements](#12-improvements-and-enhancements)
- [Section 2: Types of Errors](#section-2-types-of-errors)
    - [2.1 Structurally Unsound Errors](#21-structurally-unsound-errors)
    - [2.2 Non-Critical Errors](#22-non-critical-errors)
- [Section 3: Structurally Unsound Errors](#section-3-structurally-unsound-errors)
    - [3.1 ifil subchunk errors](#31-ifil-subchunk-errors)
    - [3.2 PHDR subchunk errors](#32-phdr-subchunk-errors)
    - [3.3 PBAG subchunk errors](#33-pbag-subchunk-errors)
    - [3.4 PMOD subchunk errors](#34-pmod-subchunk-errors)
    - [3.5 PGEN subchunk errors](#35-pgen-subchunk-errors)
    - [3.6 INST subchunk errors](#36-inst-subchunk-errors)
    - [3.7 IBAG subchunk errors](#37-ibag-subchunk-errors)
    - [3.8 IMOD subchunk errors](#38-imod-subchunk-errors)
    - [3.9 IGEN subchunk errors](#39-igen-subchunk-errors)
    - [3.10 SHDR subchunk errors](#310-shdr-subchunk-errors)
    - [3.11 Unknown subchunk errors](#311-unknown-subchunk-errors)
    - [3.12 Compressed sample errors](#312-compressed-sample-errors)
    - [3.13 ckSize errors](#313-cksize-errors)
    - [3.14 SFe64 header errors](#314-sfe64-header-errors)
- [Section 4: Non-Critical Errors](#section-4-non-critical-errors)
    - [4.1 isng subchunk errors](#41-isng-subchunk-errors)
    - [4.2 INAM, ICRD, IENG, IPRD, ICOP, ICMT or ISFT subchunk errors](#42-inam-icrd-ieng-iprd-icop-icmt-or-isft-subchunk-errors)
    - [4.3 irom or iver subchunk errors](#43-irom-or-iver-subchunk-errors)
    - [4.4 smpl, sm24 and sm32 subchunk errors](#44-smpl-smpl-sm24-and-sm32-subchunk-errors)
    - [4.5 PHDR subchunk errors](#45-phdr-subchunk-errors)
    - [4.6 PBAG subchunk errors](#46-pbag-subchunk-errors)
    - [4.7 PMOD subchunk errors](#47-pmod-subchunk-errors)
    - [4.8 PGEN subchunk errors](#48-pgen-subchunk-errors)
    - [4.9 INST subchunk errors](#49-inst-subchunk-errors)
    - [4.10 IBAG subchunk errors](#410-ibag-subchunk-errors)
    - [4.11 IMOD subchunk errors](#411-imod-subchunk-errors)
    - [4.12 IGEN subchunk errors](#412-igen-subchunk-errors)
    - [4.13 SHDR subchunk errors](#413-shdr-subchunk-errors)
    - [4.14 Undefined and unknown enum, palette value and source type errors](#414-undefined-and-unknown-enum-palette-value-and-source-type-errors)
    - [4.15 Precedence errors](#415-precedence-errors)
    - [4.16 Parameter value and terminator errors](#416-parameter-value-and-terminator-errors)
    - [4.17 Unknown chunk errors](#417-unknown-chunk-errors)
    - [4.18 Compression errors](#418-compression-errors)
    - [4.19 ISFe chunk errors](#419-isfe-chunk-errors)
    - [4.20 ifil chunk errors](#420-ifil-chunk-errors)
    - [4.21 Proprietary compression errors](#421-proprietary-compression-errors)
    - [4.22 wPreset value errors](#422-wpreset-value-errors)
    - [4.23 Duplicated preset location errors](#423-duplicated-preset-location-errors)
    - [4.24 File size limit errors](#424-file-size-limit-errors)
- [Section 5: Manual Repair](#section-5-manual-repair)
    - [5.1 Introducing manual repair](#51-introducing-manual-repair)
    - [5.2 Where should manual repair be used?](#52-where-should-manual-repair-be-used)
    - [5.3 What is repaired by manual repair?](#53-what-is-repaired-by-manual-repair)
    - [5.4 What do you need to know about manual repair as a bank developer?](#54-what-do-you-need-to-know-about-manual-repair-as-a-bank-developer)
- [Section 6: Automatic repair](#section-6-automatic-repair)
    - [6.1 Introducing automatic repair](#61-introducing-automatic-repair)
    - [6.2 Where should automatic repair be used?](#62-where-should-automatic-repair-be-used)
    - [6.3 What is repaired by automatic repair?](#63-what-is-repaired-by-automatic-repair)
    - [6.4 What is not repaired by automatic repair?](#64-what-is-not-repaired-by-automatic-repair)
    - [6.5 What do you need to know about automatic repair as a bank developer?](#65-what-do-you-need-to-know-about-automatic-repair-as-a-bank-developer)

# Section 1: Introduction

## 1.1 Scope and purpose of this document

With the increased complexity of SFe (versus SF2.04), damage to files will likely be more common. File repair programs need features to ensure that they work for their job.

In the future, this document, along with the other SFe documents, will be integrated into the SFe specification document.

## 1.2 Improvements and enhancements

The SFe file repair specification will be expanded alongside the SFe format specification.

# Section 2: Types of Errors

## 2.1 Structurally Unsound Errors

"Structurally Unsound" errors are those defined by E-mu (in legacy SF2.04), Werner Schweer (in Werner SF3) and the SFe Team (in SFe) to prevent the bank from working properly in a way that means that it can not be used. These errors must be fixed before an SF player can load it, unless the SF player implements SFe automatic repair.

## 2.2 Non-Critical Errors

"Non-critical" errors are errors that mean that data cannot be read properly, however as they are not Structurally Unsound errors, the file can be loaded. What usually happens is that the damaged data is ignored, and the rest of the bank is loaded.

While non-critical errors don't prevent the use of the bank, it is important that they are fixed to ensure that the bank functions work as intended on all SF players that conform to a specification, whether that be legacy SF 2.04, Werner SF3 or SFe.

# Section 3: Structurally Unsound Errors

## 3.1 ifil subchunk errors

If the ifil subchunk is missing, or not 4 bytes, a Structurally Unsound error occurs.

To fix this error, file repair programs must determine the correct version number of the SFe program by inspecting the file structure. File repair programs should never simply add the current SFe version, as that can cause a non-critical error relating to an ifil version mismatch.

If the file is too damaged to determine the correct ifil version, then the repair program should repair these problems first. If, after this, a definitive SF version cannot be determined, the user should be given the option to manually enter a new SF file version.

Alternatively, file repair programs can allow the user to manually enter the SF file version without allowing the program to automatically determine the necessary version.

This is applicable to SF version 2.00 and later.

## 3.2 PHDR subchunk errors

If the PHDR subchunk is missing, contains fewer than two records or not a multiple of 38 bytes, a Structurally Unsound error occurs. Such an error also occurs if the preset bag indices are not monotonic, or if there is a mismatch between the terminal preset's wPresetBagNdx and the PBAG subchunk size.

Without the PHDR subchunk, there are no presets. In the case of a missing PHDR subchunk, the program should just reconstruct an "empty" PHDR subchunk. The bank will not be usable until the PHDR subchunk is manually re-created.

If the PHDR subchunk contains at least two records, but is not a multiple of 38 bytes, then this indicates a structural error in one or more records. Each record can be inspected and the structure repaired. The user should also be given the choice between repairing the records and just deleting them. Repaired records must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

Non-monotonic preset bag indices should be reordered if encountered.

The PBAG subchunk size is usually corrected by correcting the incorrect value(s). The correct value can be reconstructed once the preset bag indices have been reordered.

This is applicable to SF version 2.00 and later.

## 3.3 PBAG subchunk errors

If the PBAG subchunk is missing or not a multiple of 4 bytes, a Structurally Unsound error occurs. Such an error also occurs if the generator or modulator indices are not monotonic, or if there is a mismatch between the generator or modulator indices and corresponding PGEN/PMOD subchunk sizes.

Without the PBAG subchunk, there are no preset zones. In the case of a missing PBAG subchunk, the program should just reconstruct an "empty" PBAG subchunk. The bank will not be usable until the PBAG subchunk is manually re-created.

If the PHDR subchunk is not a multiple of 4 bytes, or if there is a mismatch between the generator or modulator indices and corresponding PGEN/PMOD subchunk sizes, then this indicates a structural error in one or more of the preset zones. Each zone can be inspected and the structure repaired. The user should also be given the choice between repairing the zones and just deleting them. Repaired zones must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

Non-monotonic generator or modulator indices should be reordered if encountered.

The PGEN/PMOD subchunk sizes are usually corrected by correcting the incorrect value(s). The correct value can be reconstructed once the preset bag indices have been reordered.

This is applicable to SF version 2.00 and later.

## 3.4 PMOD subchunk errors

If the PMOD subchunk is missing or not a multiple of 10 bytes, a Structurally Unsound error occurs.

Without the PMOD subchunk, there are no preset modulators. In the case of a missing PMOD subchunk, the program should just reconstruct an "empty" PMOD subchunk. The bank may be usable, but there will be a significant quality loss until the PMOD subchunk is manually re-created.

If the PMOD subchunk is not a multiple of 10 bytes, then this indicates a structural error in one or more of the preset modulators. Each modulator can be inspected and the structure repaired. The user should also be given the choice between repairing the modulators and just deleting them. Repaired modulators must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

This is applicable to SF version 2.04 and later.

## 3.5 PGEN subchunk errors

If the PGEN subchunk is missing or not a multiple of 4 bytes, a Structurally Unsound error occurs. Such an error also occurs if the instrument generator value is not less than the terminal instrument.

Without the PGEN subchunk, there are no preset generators. In the case of a missing PGEN subchunk, the program should just reconstruct an "empty" PGEN subchunk. The bank will not be usable until the PGEN subchunk is manually re-created.

If the PGEN subchunk is not a multiple of 4 bytes, then this indicates a structural error in one or more of the preset generators. Each generator can be inspected and the structure repaired. The user should also be given the choice between repairing the generators and just deleting them. Repaired generators must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

The instrument generator value is usually corrected by correcting the incorrect value(s) by inspecting the structure and determining the correct value for the instrument generator value or terminal instrument.

This is applicable to SF version 2.00 and later.

## 3.6 INST subchunk errors

If the INST subchunk is missing, contains fewer than two records or not a multiple of 22 bytes, a Structurally Unsound error occurs. Such an error also occurs if the instrument bag indices are not monotonic, or if there is a mismatch between the terminal preset's wInstBagNdx and the IBAG subchunk size.

Without the INST subchunk, there are no instruments. In the case of a missing INST subchunk, the program should just reconstruct an "empty" INST subchunk. The bank will not be usable until the INST subchunk is manually re-created.

If the INST subchunk contains at least two records, but is not a multiple of 22 bytes, then this indicates a structural error in one or more records. Each record can be inspected and the structure repaired. The user should also be given the choice between repairing the records and just deleting them. Repaired records must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

Non-monotonic instrument bag indices should be reordered if encountered.

The INST subchunk size is usually corrected by correcting the incorrect value(s). The correct value can be reconstructed once the instrument bag indices have been reordered.

This is applicable to SF version 2.00 and later.

## 3.7 IBAG subchunk errors

If the IBAG subchunk is missing or not a multiple of 4 bytes, a Structurally Unsound error occurs. Such an error also occurs if the generator or modulator indices are not monotonic, or if there is a mismatch between the generator or modulator indices and corresponding IGEN/IMOD subchunk sizes.

Without the IBAG subchunk, there are no instrument zones. In the case of a missing IBAG subchunk, the program should just reconstruct an "empty" IBAG subchunk. The bank will not be usable until the IBAG subchunk is manually re-created.

If the IHDR subchunk is not a multiple of 4 bytes, or if there is a mismatch between the generator or modulator indices and corresponding IGEN/IMOD subchunk sizes, then this indicates a structural error in one or more of the instrument zones. Each zone can be inspected and the structure repaired. The user should also be given the choice between repairing the zones and just deleting them. Repaired zones must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

Non-monotonic generator or modulator indices should be reordered if encountered.

The IGEN/IMOD subchunk sizes are usually corrected by correcting the incorrect value(s). The correct value can be reconstructed once the instrument bag indices have been reordered.

This is applicable to SF version 2.00 and later.

## 3.8 IMOD subchunk errors

If the IMOD subchunk is missing or not a multiple of 10 bytes, a Structurally Unsound error occurs.

Without the IMOD subchunk, there are no instrument modulators. In the case of a missing IMOD subchunk, the program should just reconstruct an "empty" IMOD subchunk. The bank may be usable, but there will be a significant quality loss until the IMOD subchunk is manually re-created.

If the IMOD subchunk is not a multiple of 10 bytes, then this indicates a structural error in one or more of the instrument modulators. Each modulator can be inspected and the structure repaired. The user should also be given the choice between repairing the modulators and just deleting them. Repaired modulators must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

This is applicable to SF version 2.04 and later.

## 3.9 IGEN subchunk errors

If the IGEN subchunk is missing or not a multiple of 4 bytes, a Structurally Unsound error occurs. Such an error also occurs if the sampleID generator value is not less than the terminal sampleID.

Without the IGEN subchunk, there are no instrument generators. In the case of a missing IGEN subchunk, the program should just reconstruct an "empty" IGEN subchunk. The bank will not be usable until the IGEN subchunk is manually re-created.

If the IGEN subchunk is not a multiple of 4 bytes, then this indicates a structural error in one or more of the instrument generators. Each generator can be inspected and the structure repaired. The user should also be given the choice between repairing the generators and just deleting them. Repaired generators must be indicated so the user can make any required adjustments. This does not have to be in the file, rather just in the user interface of the program.

The sampleID generator value is usually corrected by correcting the incorrect value(s) by inspecting the structure and determining the correct value for the sampleID generator value or terminal sampleID.

This is applicable to SF version 2.00 and later.

## 3.10 SHDR subchunk errors

If the SHDR subchunk is missing or not a multiple of 46 bytes, a Structurally Unsound error occurs. Such an error also occurs if a sample is flagged as a ROM sample but there is no valid "irom" subchunk.

Without the SHDR subchunk, there are no defined samples. If there is no usable sample data, the program should just reconstruct an "empty" SHDR subchunk. However, if there is usable sample data, the program may attempt to partially reconstruct the SHDR subchunk. User input will be required.

If there is no valid "irom" subchunk, the program can clean these samples if they aren't being used in the bank. If they are used by the bank, then the program should then attempt to read the sample as a non-ROM sample, and if the samples are valid, then this means that the problem is fixed. If there is no valid sample, then either a new sample must be provided by the user, or a ROM should be defined for the irom subchunk.

This is applicable to SF version 2.00 and later.

## 3.11 Unknown subchunk errors

If there are any unknown subchunks in the pdta-info chunk, a Structurally Unsound error occurs.

These errors can easily be fixed; the unknown subchunks are simply removed.

This is applicable to SF version 2.00 and later.

## 3.12 Compressed sample errors

If there are PCM samples after compressed samples, a Structurally Unsound error occurs.

In Werner SF3, all PCM samples must go before compressed samples. This is fixed by rearranging the sample data in the smpl chunk, and then updating the SHDR subchunk.

This is applicable to SF version 3.00 and later.

## 3.13 ckSize errors

For SFe32, if the value of ckSize is 4,294,967,295 or another inaccurate value, a Structurally Unsound error occurs. For SFe64, if the value of ckSize is not 4,294,967,295, a Structurally Unsound error occurs.

This is easily solved by checking the ckSize values and fixing them with the correct file sizes, and in the case of SFe64, setting the ds64 chunk size to the correct value.

This is applicable to SF version 4.00 and later.

## 3.14 SFe64 header errors

If there is an SFe32 header in an SFe64 file, a Structurally Unsound error occurs.

This is easily solved by replacing the SFe32 header with an SFe64 header.

This is applicable to SFe64 only, version 4.00 and later.

# Section 4: Non-Critical Errors

## 4.1 isng subchunk errors

If the isng subchunk is missing or is not terminated by a zero-valued byte, an SFe player that doesn't implement automatic repair will assume its default sound engine value. For legacy SF 2.04 and Werner SF3, this value is "EMU8000", and for SFe 4.00 and later, this is "SFeXX version Y" where XX is the SFe type and Y is the version number.

&nbsp;In the case of a missing isng subchunk, the value to use depends on the ifil value:

- If ifil=2.00 or 3.00, use "EMU8000".
- If ifil=2.01 or 3.01, use "E-mu 10K1" or "E-mu 10K2".
- If ifil=2.04 or 3.04, use "X-Fi".
- If ifil=2.128, 3.128, 4.00 or higher, use "SFeXX version Y", where XX is the SFe type and Y is the version number.

If not terminated by a zero-valued byte, then add a zero-valued byte and warn the user to verify if the value is correct.

This is applicable to SF version 2.00 and later.

## 4.2 INAM, ICRD, IENG, IPRD, ICOP, ICMT or ISFT subchunk errors

If any of these subchunks are missing, not terminated by a zero-valued byte, or cannot be faithfully copied as a string in the format declared by the specification, the value is ignored.

Missing subchunks should be filled in intuitively. For example, for an INAM subchunk, the file name or "Unnamed bank" are good starting points.

If not terminated by a zero-valued byte, then add a zero-valued byte and warn the user to verify if the value is correct.

With the exception of the INAM chunk, if the subchunk's value cannot be faithfully copied as a string, the user should be given a chance to add the correct value. The format declared by the specification is:

- If wMajor=2 or 3, then these strings are in Ascii format.
- If wMajor=4 or greater, then these strings are in UTF-8 format.

This is applicable to SF version 2.00 and later.

## 4.3 irom or iver subchunk errors

If any of these subchunks are missing, not terminated by a zero-valued byte, or refer to an unknown or incorrect ROM, the value is ignored.

Missing subchunks should not be filled in unless there are ROM samples that are linked.

This is applicable to SF version 2.00 and later.

## 4.4 smpl, sm24 and sm32 subchunk errors

If the smpl subchunk is missing, and there are no ROM samples, then there are no samples, however technically this is allowed by the specification. However, if the smpl subchunk is missing, but the sm24 and/or sm32 subchunks are present, then an error may occur. The sm24 subchunk is only supported in legacy SF 2.04, Werner SF3 and SFe, and the sm32 subchunk is only supported in SFe, so if these subchunks appear with a bad ifil version, anything there is ignored.

If only the sm24 subchunk is present, then 8-bit sample operation is enabled, and there is no error. However, if only the sm32 subchunk is present, then the sm32 subchunk should be renamed to sm24, enabling standard 8-bit sample operation. 8-bit sample operation is only supported in SFe.

If both the sm24 and sm32 subchunks are present, then these subchunks should be combined into 16-bit samples in one smpl subchunk. Because endianness may not be clear in this situation, you must allow the user to select the endianness of the operation.

If there is a mismatch in the ifil version and the presence of sm24 and/or sm32 subchunks, then allow the user to select whether they want to keep these subchunks and update the ifil version to the correct value, or if they want to remove it while retaining the existing ifil value.

This is applicable to SF version 2.04 and later.

## 4.5 PHDR subchunk errors

If a wBank value is invalid (legacy SF2.0x only), a preset was found with no zones, or a value of dwLibrary (legacy SF2.0x only), dwGenre (legacy SF2.0x only), or dwMorphology, then these values are ignored.

For legacy SF2.0x, invalid wBank values should be detected, and the user should be given the choice to select a correct value, or to update the ifil version to one that represents SFe instead.

Because dwLibrary and dwGenre were reserved in legacy SF2.0x, the user should be given the choice to clear the values, or to update the ifil version to one that represents SFe instead. Any dwMorphology value should be cleared because current versions of SFe do not implement this yet.

This is applicable to SF version 2.00 and later.

## 4.6 PBAG subchunk errors

If a zone after the first lacks an instrument generator as its last generator, or if a global zone lacks a modulator or generator, an SFe player that doesn't implement automatic repair will ignore the zone.

These problems can easily be fixed by giving zones after the first (including the global zone) an instrument generator.

This is applicable to SF version 2.00 and later.

## 4.7 PMOD subchunk errors

If the values of sfModSrcOper, sfModDestOper or sfModTransOper are unknown, if sfModSrcOper is set to "link" without another linked modulator, or sfModAmtSrcOper is set to "link", an SFe player that doesn't implement automatic repair will ignore the modulator. A modulator that has links to a modulator index exceeding the total number of modulators, is circularly linked to other modulators, or with the same three enumerators as another modulator, would also be ignored.

To fix unknown or inappropriate "link" values, they should be corrected to a value given by the user. Out-of-range modulator indexes should be fixed by letting the user select the correct modulator, or define a new modulator if it doesn't exist. Circularly linked modulators should be highlighted to allow the user to break the circular links. Modulators with the same enumerators should also be highlighted, so the enumerators can be changed by the user.

This is applicable to SF version 2.04 and later.

## 4.8 PGEN subchunk errors

If the value of sfGenOper is unknown, or if the modulator was found with the same sfGenOper enumerator as another modulator, an SFe player that doesn't implement automatic repair will ignore the generator. Generators found after an instrument generator, velocity range modulators found after non-key range modulators, or non-global lists not ending in an instrument generator will also be ignored.

Unknown sfGenOper values should be corrected to a value given by the user. Modulators with the same sfGenOper enumerator as another modulator should be highlighted, so it can be changed by the user. Generators and modulators in inappropriate places should also be moved with references corrected. Non-global lists that don't have an instrument generator at the end should have an instrument generator added.

This is applicable to SF version 2.00 and later.

## 4.9 INST subchunk errors

If an instrument is found with no zones, then an SFe player that doesn't implement automatic repair will ignore the instrument.

To fix this issue, the instrument should be deleted unless it's being used by a preset. If so, the instrument should be kept, but the user should be warned so they can fix the problem.

This is applicable to SF version 2.00 and later.

## 4.10 IBAG subchunk errors

If a zone after the first lacks a sampleID generator as its last generator, or if a global zone lacks a modulator or generator, an SFe player that doesn't implement automatic repair will ignore the zone.

These problems can easily be fixed by giving zones after the first (including the global zone) a sampleID generator.

This is applicable to SF version 2.00 and later.

## 4.11 IMOD subchunk errors

If the values of sfModSrcOper, sfModDestOper or sfModTransOper are unknown, if sfModSrcOper is set to "link" without another linked modulator, or sfModAmtOper is set to "link", an SFe player that doesn't implement automatic repair will ignore the modulator. A modulator that has links to a modulator index exceeding the total number of modulators, is circularly linked to other modulators, or with the same three enumerators as another modulator, would also be ignored.

To fix unknown or inappropriate "link" values, they should be corrected to a value given by the user. Out-of-range modulator indexes should be fixed by letting the user select the correct modulator, or define a new modulator if it doesn't exist. Circularly linked modulators should be highlighted to allow the user to break the circular links. Modulators with the same enumerators should also be highlighted, so the enumerators can be changed by the user.

This is applicable to SF version 2.04 and later.

## 4.12 IGEN subchunk errors

If the value of sfGenOper is unknown, or if the modulator was found with the same sfGenOper enumerator as another modulator, an SFe player that doesn't implement automatic repair will ignore the generator. Generators found after a sampleID generator, velocity range modulators found after non-key range modulators, or non-global lists not ending in an sampleID generator will also be ignored.

Unknown sfGenOper values should be corrected to a value given by the user. Modulators with the same sfGenOper enumerator as another modulator should be highlighted, so it can be changed by the user. Generators and modulators in inappropriate places should also be moved with references corrected. Non-global lists that don't have a sampleID generator at the end should have an sampleID generator added.

This is applicable to SF version 2.00 and later.

## 4.13 SHDR subchunk errors

If there is a zero sample rate, a bad original pitch value (128-254) or a non-zero wSampleLink value with a mono sfSampleType, then an SFe player that doesn't implement automatic repair will ignore these values. Samples without enough leeway as defined by SFSPEC24.PDF or with a sample rate outside of the reproducible range may also be ignored on legacy SF 2.0x.

If the sample rate is zero, then it should be corrected automatically to the correct value via automatic pitch detection and then highlighted for the user to verify. Bad original pitch values should be corrected to the value with automatic pitch detection. Non-zero wSampleLink values should be set to zero. For legacy SF 2.0x, sample leeway can be added (if the situation permits), and the sample rate can be reset to a reproducible value.

For SFe, you must not edit the sample rate unless it is zero.

This is applicable to SF version 2.00 and later.

## 4.14 Undefined and unknown enum, palette value and source type errors

If enumerators, palette values or source types are undefined or unknown, then they are ignored.

Anything that uses these values should either be removed or highlighted so the user can inspect it. If a value is undefined for the ifil version, but defined for a newer version, then the program can also offer to update the version to a newer version.

This is applicable to SF version 2.00 and later.

## 4.15 Precedence errors

If an attempt was made to use a generator only available at the instrument level in the preset level, then the generator is ignored.

In this case, the user should be allowed to change the generator value or to remove the offending generator entirely.

This is applicable to SF version 2.00 and later.

## 4.16 Parameter value and terminator errors

If a parameter value is illegal, or if parameters or terminators are missing, then anything that requires these parameters or terminators may be ignored.

In this case, the illegal or missing parameter value should be shown to the user, so they can rectify it. Terminators should automatically be added wherever possible.

This is applicable to SF version 2.00 and later.

## 4.17 Unknown chunk errors

If chunks in the INFO-list or sdta-list are unknown, then they are ignored.

If a chunk is undefined in the ifil version given, but defined in a later version, then the ifil version should be updated. If it is undefined in any version, then it can safely be deleted.

This is applicable to SF version 2.00 and later.

## 4.18 Compression errors

If a compressed sample is invalid according to the Werner SF3 specification, or if wSampleLink is non-zero for a compressed sample, then the compressed sample is ignored. This can also happen if the program is unable to decompress the sample.

The user should be given the choice of compression algorithms to use for the sample, and wSampleLink values should be set to zero.

This is applicable to SF version 3.00 and later.

## 4.19 ISFe chunk errors

If the ISFe chunk is missing or corrupted, then important information relating to features introduced in SFe may be missing.

The ISFe chunk can be repaired, however information in the ISFe chunk should be reconstructed.

This is applicable to SF version 4.00 and later.

## 4.20 ifil chunk errors

The ifil chunk should always match the features that are used in the bank. Otherwise, features may not operate as expected. SFe programs that implement automatic repair should ignore the ifil version if it's incorrect, and instead use the correct determined version.

If features or feature flags from a newer ifil version of SFe are found on a bank with an older declared version of ifil, then the version should be updated to the detected version of ifil.

This is applicable to SF version 4.00 and later.

## 4.21 Proprietary compression errors

To make life easier for end-users of SFe banks, proprietary compression formats (such as sfArk, SFPack, SF2Pack and sfq) are prohibited.

If a proprietary compression format is supported by the SFe program, then it should be decompressed and automatically recompressed into a lossless format using Werner SF3.

This is applicable to SF version 4.00 and later.

## 4.22 wPreset value errors

With SFe, more wPreset values will be defined. If wPreset values aren't defined, then they will not be accessible.

If such presets are found, then they should be highlighted by the program, and the user should have the opportunity to select a different wPreset value.

This is applicable to SF version 4.00 and later.

## 4.23 Duplicated preset location errors

If a preset location is duplicated, then there could be issues with using the bank.

Duplicated preset locations should be highlighted, and the user should have the opportunity to select a different preset value.

This is applicable to SF version 4.00 and later.

## 4.24 File size limit errors

If the file size limit of SFe is exceeded, then it can result in file corruption. Therefore, it is necessary to refrain from exceeding 4 GiB when using SFe32.

SFe32 headers and structures can be replaced with SFe64 (and in the future SFe64L) if the file size was found to exceed 4 GiB. Alternatively, if TSC mode is supported by the SFe program, then it can be activated by moving the sdta-info chunk to the end and setting the correct feature flag in the ISFe subchunk.

This is applicable to SF version 4.00 and later.

# Section 5: Manual Repair

## 5.1 Introducing manual repair

Manual repair is used to completely fix a broken SFe bank. It can be partially automated, however some parts of manual repair are not automatable, and the parts that aren't automatable are highlighted.

## 5.2 Where should manual repair be used?

Manual repair is intended to be part of SFe bank development tools such as SFe editors or dedicated file repair programs. It is also suitable for situations where control over the repair process by the user is required. However, it is not suitable for SF players.

## 5.3 What is repaired by manual repair?

Manual repair can be used to repair all Structurally Unsound errors and non-critical errors listed in section 3. This is the main advantage that it holds over automatic repair.

## 5.4 What do you need to know about manual repair as a bank developer?

You can use it to fix a corrupted bank. A manual repair program is very useful if you develop banks, as your data may be damaged at any time for any reason.

# Section 6: Automatic repair

## 6.1 Introducing automatic repair

Automatic repair allows SFe players to play some "Structurally Unsound" banks by automatically repairing them at load time. It consists of a partial file repair program built directly into the SFe player. With future versions of this specification, SFe64 players that only support a higher version of the format will also gain the ability to translate old banks to run properly.

## 6.2 Where should automatic repair be used?

Automatic repair is intended to be part of SFe players. It is an aid to help SFe players play banks that are otherwise "Structurally Unsound". It is not a substitute for repairing the bank using file repair programs. File repair programs should always include an option to use manual repair.

## 6.3 What is repaired by automatic repair?

Automatic repair fixes structural defects in SFe and SF2.04 banks seamlessly and transparently. It should automatically repair all Structurally Unsound errors listed in section 3 except for "3.12 Compressed sample errors" and anything that requires user input.

It should also repair all non-critical errors listed in section 4 except for "4.18 Compression errors", "4.22 wPreset value errors", "4.24 File size limit errors" and anything that requires user input. The repair of "4.21 Proprietary compression errors" is optional and contingent on support for such formats.

The program developers are allowed to use any repair strategy listed in sections 3 and 4.

Automatic repair requires that the implementation give a message when invoked. This is to encourage bank developers not to rely on the feature to implicitly define any parameters.

## 6.4 What is not repaired by automatic repair?

Automatic repair is a great method to fix issues that prevent SF banks from loading correctly, but it can't repair all defects. For example, anything that requires user input is outside of the scope of automatic repair, and should be dealt with by a file repair program or SFe editor program instead.

This feature must also never overwrite files. This is the job of a file repair program. If system memory is low, it is acceptable for automatic repair implementations to create a patched bank in temporary file storage.

## 6.5 What do you need to know about automatic repair as a bank developer?

You must correctly setup your banks to ensure that they run properly; do not use automatic repair to implicitly define certain parameters. If you do so, then your bank may not run properly on a legacy SF player or an SFe player that doesn't implement automatic repair.

&nbsp;