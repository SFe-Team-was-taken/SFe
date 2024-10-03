# Section 10: Error-handling

## 10.1 Structural errors

The error correction process for structural errors in SFe32 is largely similar to the process in older versions of the format.

* * *

## 10.1a Duplicated preset locations within files

This occurs when the file is structurally damaged or manually edited in a manner where more than one preset has the same value of wBank and wPreset (for instance, 015:000:081).

- In SoundFont(R) 2.04, the first preset in the location would be used by default, but the other presets would still be retained.
- Such other presets must be moved before they can be used.
- In SFe, the preset to be used is no longer necessarily the first one. Instead, selecting the correct preset (or combination of presets) to use will be permissible.
- Such a feature is optional, and if not implemented, the player should use the SF2.04 behaviour in these cases (use the first preset found).
- Editors should warn the user if such presets are found.
- This behaviour might change in future versions, so please take the "ifil" value, and later versions of this specification, into account. In particular, later versions of SFe32 will use the ISFe sub-chunk to determine this behaviour.

* * *

## 10.1b Duplicated preset locations across files

This occurs when multiple files are loaded simultaneously (now a required feature for SFe), but some or all of the files have presets with identical wBank and wPreset values.

- Behaviour was undefined in SoundFont(R) 2.04.
- This was because multiple file loading was not a standard feature that was mandated in the legacy SoundFont(R) standard.
- SF version 2 and 3 compatible software developers therefore had the liberty to implement multiple file loading however they wanted to.
- This edge case will now be defined in SFe.
- If multiple presets across loaded files have the same value of wBank and wPreset, then the preset to be used may be selectable from all the presets with the same bank location, depending on the player implementation. The preset to be used may also be a combination of multiple presets.
- Such a feature is also optional, and if not implemented, you can either use the first preset found, or you can combine all the presets.
- While initially intended to enable the creation of instruments with extremely large file size (beyond 4GiB), or use a massive number of generators (beyond 65536), with the SFe32 format, other methods, such as SiliconSFe Linking, are now preferred. However, such SFe32 files may not play correctly on legacy SF version 2 or 3 players.
- This behaviour might change in future versions, so please note the "ifil" value, and later versions of this specification, into account. In particular, later versions of SFe will use the ISFe sub-chunk to determine this behaviour.

* * *

## 10.2 Undefined chunks

SoundFont(R) 2.04 players should ignore SFe-specific sub-chunks, as prescribed by the legacy SoundFont(R) 2.04 specification.

Also, SFe version 4.00 compatible players, which do not support future versions, should ignore sub-chunks which are used in future versions.

* * *

## 10.3 Unknown Enumerators

Any ifil versions of 4.01 or above may have unknown enumeration values for a version 4.00 player.

This is entirely expected, and if unknown enumeration values are found, the Generator/Modulator should be ignored.

* * *

## 10.4 Illegal Parameter Values

Illegal parameter values are handled as in SoundFont(R) 2.04.

* * *

## 10.5 Out of Range Values

Out of range values are be handled as in SoundFont(R) 2.04.

* * *

## 10.5a Exceeded Maximum File Size Limit

This occurs when the user loads a file that is larger than the maximum size that the SFe program can accommodate.

- In the AWE32 and AWE64, the limit was dependent on the memory installed on the card, which was up to 28 MiB.
- Later sound cards allowed the user to load files with file sizes up to system memory.
- SFe32 has defined limits that are found in the separate program specification.
- If these limits are reached, you can reject loading of the file with an error, or attempt to load the file anyway.
- SFe32 programs should warn the user if processing was automatically done to a file to reduce the file size to be in range.
- If multiple files are loaded, and the limit is reached, the order of files to be loaded can be defined by the author of the SFe32 compatible software.

* * *

## 10.6 Missing Required Items

If required items are missing, it is handled as in SoundFont(R) 2.04.

* * *

## 10.7 Illegal Enumerators

Illegal enumerators are handled as in SoundFont(R) 2.04.