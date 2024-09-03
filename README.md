# SF-enhanced (SFe)

## Bringing soundfonts to new heights

### This is the SFe64-only branch.

This is a version of the SFe specification which only includes the parts of the spec that are relevant to SFe64. We plan on making major changes to this spec in the future, so the separation of the SFe32 and SFe64 specs will make it clearer.

In particular, we are planning on making SFe64 version 4 files readable as SFe32 files if below 4 GiB. If this change is made, then:

- we will branch off SFe64 version 5.00 from 4.00.
- the spec in this branch will refer to version 5.00, with a new branch for version 4.00.
- version 5.00 will release after version 4.01, the furthest planned release for SFe version 4.
- this spec will become incompatible with SFe64 version 4.00.
- a new variant of SFe, codenamed "SFe64L", will be limited to the SFe32 features and 64-bit support.
- features can more easily be added to SFe64 independently of SFe32 and "SFe64L".

---

### What is SFe?

Like many members of the soundfont community, we are tired of the limitations of the ancient SoundFont format. So, in 2020, we launched the SFe (SF-enhanced) project, to research backwards-compatible improvements and updates to the format.

To do this, we looked at many features that soundfont creators have requested, and are working on incorporating them into the SFe format.

### What are the goals of SFe?

The goals of the SFe project are to:

- Unite proprietary extensions to the SoundFont format
- Add the most requested features by soundfont developers
- Enable sample libraries that we could never have imagined 
- Create a viable competitor to commercial sample library formats (Kontakt, etc.)
- Allow intercompatibility between other open source sample library formats (such as SFZ)

### When will the specification become available?

We will release the specification when it's done. In the meanwhile, we will regularly release drafts of the SFe specification.

### Why does the specification not include everything?

To make it more concise, we only highlight the differences between the SFe specification and the legacy SoundFont specification (sfspec24). If you want to develop for SFe, we recommend that you also read the legacy SF specification (sfspec24).

### How can I contribute?

If you have a proposal for how we could implement a new feature, then you can fork this repository and then create a pull request. 

If you've got an idea, but don't know how to implement it, then add an issue and describe what feature you want to see, and then we should respond to this proposal when we have time.

