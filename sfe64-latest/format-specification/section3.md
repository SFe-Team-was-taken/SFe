# Section 3: RIFF and RF64 structure

## 3.1 General RIFF and RF64 file structures

### The RIFF format is the file format used in the Soundfont(r) 2.x and Werner SF3 standards, and in SFe32.

### The RIFF64 format (also called RF64) is the file format used in SFe64. It is compatible with RIFF.

Both RIFF and RIFF64 are created in building blocks known as "chunks".

Chunks are defined using this structure:

- A unique four character code.
- "ckID": type of data in chunk
- "ckSize": size of chunk (SFe32), equal to 4,294,967,295 (SFe64)
- "ds64": size of chunk (SFe64)
- "ckDATA\[ckSize\]": the data inside the chunks, including pad bytes.

Chunks can be further divided into "sub-chunks".

Orders of chunks in all SF files are strictly defined, as in versions 2 and 3, and should be kept to, with the exception of TSC mode.

* * *

## 3.2 Chunks and subchunks in version 4

Like SoundFont(R) 2.04, there are 3 main chunks:

1.  "INFO" Chunk: contains important information about the soundfont.
    
2.  "sdta" Chunk: A single sub-chunk containing audio samples.
    
3.  "pdta" Chunk: Nine sub-chunks (in the "Hydra" structure, named after a many headed beast) containing the parameters about how the audio samples should be played. (According to E-mu, the hydra has nine heads. Cut one off, and another two grow.)
    

The 3 main chunks should appear in this order, and the nine sub-chunks of the "pdta" chunk should appear in the order described.

* * *

## 3.3 Error handling

The RIFF and RF64 formats have error checking features about:

- The size of the file
- The length of the chunks
- The length of the sub-chunks

Using this information, it is possible to check for damage to a SF file:

- If any damage is detected due to such a mismatch, the file should be rejected as "Structurally Unsound".
- Like E-mu(r) Soundfont(r) 2.x and Werner SF3, developers can create programs which correct "Structurally Unsound" files of version 4 and later.
- A specification for such a program will be ready for 4.00.7.