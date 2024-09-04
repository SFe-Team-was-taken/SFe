# Section 4: RIFF file format of SFe32, version 4.00

## 4.1-4.4 File structure of SFe32, version 4.00

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

* * *

## 4.5 Type definitions

The type definitions are identical to those used in SoundFont(R) version 2.04.

* * *

## 4.5a File format extensions

SFe32 files should use file extension .SFE32 if incompatible with legacy SF players, but use .SF2 or .SF3 if compatible.