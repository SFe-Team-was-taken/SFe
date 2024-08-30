# Section 4: RIFF and RF64 file format of version 4

## 4.1-4.4 File structure of version 4

SFe32 file structure:

```
RIFF('sfbk'
        {
        LIST('INFO'
            {
            ifil(
                struct sfVersionTag
                {
                    WORD wMajor;
                    WORD wMinor;
                };
            )
            isng(szSoundEngine:ZSTR)
            INAM(szName:ZSTR)
            ICRD(szDate:ZSTR)
            IENG(szName:ZSTR)
            IPRD(szProduct:ZSTR)
            ICOP(szCopyright:ZSTR)
            ICMT(szComment:ZSTR)
            ISFT(szTools:ZSTR)
            }
            )
        )
        LIST('sdta'
            {
            smpl([sample:SHORT])
            }
            {
            sm24([sample:CHAR])
            }
            {
            sm32([sample:CHAR])
            }
        )
        LIST('pdta'
            {
            phdr(
                struct sfPresetHeader
                {
                    CHAR achPresetName[20];
                    WORD wPreset;
                    WORD wBank;
                    DWORD dwPresetBagNdx;
                    DWORD dwLibrary;
                    DWORD dwGenre;
                };
            )
            pbag(
                struct sfPresetBag
                {
                    WORD wGenNdx;
                    WORD wModNdx;
                };
            )
            pmod(
                struct sfModList
                {
                    SFModulator sfModSrcOper;
                    SFModulator sfModDestOper;
                    SHORT modAmount;
                    SFModulator sfModAmtSrcOper;
                    SFTransform sfModTransOper;
                };
            )
            pgen(
                struct sfGenList
                {
                    SFGenerator sfGenOper;
                    genAmountType genAmount;
                };
            )
            inst(
                struct sfInst
                {
                    CHAR achInstName[20];
                    WORD wInstBagNdx;
                };
            )
            ibag(
                struct sfInstBag
                {
                    WORD wInstGenNdx;
                    WORD wInstModNdx;
                };
            )
            imod(
                struct sfModList
                {
                    SFModulator sfModSrcOper;
                    SFModulator sfModDestOper;
                    SHORT modAmount;
                    SFModulator sfModAmtSrcOper;
                    SFTransform sfModTransOper;
                };
            )
            igen(
                struct sfGenList
                {
                    SFGenerator sfGenOper;
                    genAmountType genAmount;
                };
            )
            shdr(
                struct sfSample
                {
                    CHAR achSampleName[20];
                    CHAR achSampleDescription[256];
                    DWORD dwStart;
                    DWORD dwEnd;
                    DWORD dwStartloop;
                    DWORD dwEndloop;
                    DWORD dwStartloop2;
                    DWORD dwEndloop2;
                    DWORD dwStartloop3;
                    DWORD dwEndloop3;
                    DWORD dwStartloop4;
                    DWORD dwEndloop4;
                    DWORD dwStartloop5;
                    DWORD dwEndloop5;
                    DWORD dwStartloop6;
                    DWORD dwEndloop6;
                    DWORD dwStartloop7;
                    DWORD dwEndloop7;
                    DWORD dwStartloop8;
                    DWORD dwEndloop8;
                    DWORD dwSampleRate;
                    BYTE byOriginalKey;
                    CHAR chCorrection;
                    DWORD dwSampleLink;
                    SFSampleLink sfSampleType;
                };
            )
            }
        )
    )
```

SFe64 file structure:

```
BW64('sfbk'
        {
        ds64([Size of SF3 64-Bit File])
        LIST('INFO'
            {
            ifil(
                struct sfVersionTag
                {
                    WORD wMajor;
                    WORD wMinor;
                };
            )
            isng(szSoundEngine:ZSTR)
            INAM(szName:ZSTR)
            ICRD(szDate:ZSTR)
            IENG(szName:ZSTR)
            IPRD(szProduct:ZSTR)
            ICOP(szCopyright:ZSTR)
            ICMT(szComment:ZSTR)
            ISFT(szTools:ZSTR)
            }
            )
        )
        LIST('sdta'
            {
            smpl([sample:SHORT])
            }
            {
            sm24([sample:CHAR])
            }
            {
            sm32([sample:CHAR])
            }
        )
        LIST('pdta'
            {
            phdr(
                struct sfPresetHeader
                {
                    CHAR achPresetName[256];
                    CHAR achSampleDescription[256];
                    WORD wPreset;
                    WORD wBank;
                    DWORD dwPresetBagNdx;
                    DWORD dwLibrary;
                    DWORD dwGenre;
                };
            )
            pbag(
                struct sfPresetBag
                {
                    DWORD dwGenNdx;
                    DWORD dwModNdx;
                };
            )
            pmod(
                struct sfModList
                {
                    SFModulator sfModSrcOper;
                    SFModulator sfModDestOper;
                    LONG modAmount;
                    SFModulator sfModAmtSrcOper;
                    SFTransform sfModTransOper;
                };
            )
            pgen(
                struct sfGenList
                {
                    SFGenerator sfGenOper;
                    genAmountType genAmount;
                };
            )
            inst(
                struct sfInst
                {
                    CHAR achInstName[256];
                    DWORD dwInstBagNdx;
                };
            )
            ibag(
                struct sfInstBag
                {
                    DWORD dwInstGenNdx;
                    DWORD dwInstModNdx;
                };
            )
            imod(
                struct sfModList
                {
                    SFModulator sfModSrcOper;
                    SFModulator sfModDestOper;
                    LONG modAmount;
                    SFModulator sfModAmtSrcOper;
                    SFTransform sfModTransOper;
                };
            )
            igen(
                struct sfGenList
                {
                    SFGenerator sfGenOper;
                    genAmountType genAmount;
                };
            )
            shdr(
                struct sfSample
                {
                    CHAR achSampleName[256]
                    QWORD qwStart;
                    QWORD qwEnd;
                    QWORD qwStartloop;
                    QWORD qwEndloop;
                    QWORD qwStartloop2;
                    QWORD qwEndloop2;
                    QWORD qwStartloop3;
                    QWORD qwEndloop3;
                    QWORD qwStartloop4;
                    QWORD qwEndloop4;
                    QWORD qwStartloop5;
                    QWORD qwEndloop5;
                    QWORD qwStartloop6;
                    QWORD qwEndloop6;
                    QWORD qwStartloop7;
                    QWORD qwEndloop7;
                    QWORD qwStartloop8;
                    QWORD qwEndloop8;
                    QWORD qwSampleRate;
                    BYTE byOriginalKey;
                    CHAR chCorrection;
                    QWORD qwSampleLink;
                    SFSampleLink sfSampleType;
                };
            )
            }
        )
    )
```

* * *

## 4.5 Type definitions

"GenAmountType" has been increased from 16-bit to 32-bit. (SFe64)

- The limit for IGen/PGen values is now 4,294,967,296 Generators.
- Achieved by adding two more BYTE values, "by24" and "by32".
- These new BYTE values are used to describe the top 16 bits of the new 32-Bit system.
- These should be ignored by systems which do not support version 4.

```
typedef struct
    {
        BYTE byLo;
        BYTE byHi;
        BYTE by24;
        BYTE by32;
    } rangestype;

    typedef union
    {
        rangesType ranges;
        SHORT shAmount;
        LONG lngAmount;
        WORD wAmount;
        DWORD dwAmount;
    } genAmountType;
```

The SFSampleLink enum is identical to the one used in SoundFont(R) version 2.04.

* * *

SFe64 files may use the extension .SF64 or .SFE64 if desired, to prevent playback in legacy SF players that do not support SFe64.

SFe32 files should retain the extension .SF2 (or .SF3), but other conventions used should continue. The file extensions .SF32 and .SFE32 are not recommended, but players should recognise them.

The file extensions .SFE and .SF4 shall be recognised; players should check to see if such a file is either SFe32 or SFe64, and adapt accordingly.