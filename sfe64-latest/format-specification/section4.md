# Section 4: RF64 file format of SFe64, version 4.00

## 4.1-4.4 File structure of version 4

SFe64 file structure:

```
BW64('sfbk'
        {
        ds64([Size of SFe64 File])
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
                    DWORD dwStart;
                    DWORD dwEnd;
                    DWORD dwStartloop;
                    DWORD dwEndloop;
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

* * *

## 4.5 Type definitions

The type definitions are identical to those used in SoundFont(R) version 2.04.

* * *

## 4.5a File format extensions

SFe64 files may use the extension .SFE64 to prevent playback in legacy SF players that do not support SFe64.