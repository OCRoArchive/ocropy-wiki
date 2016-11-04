This wiki site is based on https://docs.google.com/document/d/1czzhPZdQRs5vENwftHGt608BS1Y7Jj2f5ZZIkuSKP8A/preview#, discussed in [issue #126](https://github.com/tmbdev/ocropy/issues/126)

## Binary Page Images

File Names: basename.bin.png

Low-Level Format: PNG24

A binarized page image.


## Physical Layout

File Names: basename.pseg.png

Low-Level Format: PNG24

Physical layout analysis represents the division of a document page into special areas, columns, paragraphs, and text lines.
This format is intended to represent with pixel-accuracy the results of “classical”, non-probabilistic physical layout analysis.
These divisions are encoded as follows into the format:
* R channel “columns”
  * R=0: reserved
  * R=1…31: the column number of the pixel
  * R=32…254: reserved
  * R=254: elements spanning multiple columns
  * R=255: special blocks (page numbers, etc.)
* G channel “paragraphs”
  * G=0…63
    * if the segmenter detects paragraphs, the paragraph number of the pixel, counted within its column
      * G=0 cannot occur in this case (since paragraphs are counted starting from 1)
    * if the segmenter doesn't detect paragraphs, the upper 6 bits of the line number within the column
      * G=0 can occur in this case
  * G=64…249: reserved
  * G=250: horizontal/vertical ruling
  * G=251: sidebar
  * G=252: caption
  * G=253: table
  * G=254: non-continuous tone image, line drawing
  * G=255: continuous tone image
* B channel “line numbers”
  * if the containing element is a paragraph, B=1…255: the line number within its paragraph (B=0 cannot occur)
  * if the containing element is a column (with no paragraph detection), the lower 8 bit of the line number (R=0 and B=0 cannot occur simultanously)
  * if the element is an image, table, etc., the number within the column in reading order (B=0 is illegal)

The following special RGB values are recognized:
* (255,1,*): page number region
* (255,2,*): running header (excluding page number)
* (255,3,*): running footer (excluding page number)
* (255,255,0): noise pixels
* (255,255,128): white space layout element
* (255,255,255): unclassified page background
* (0,0,0): reserved; no page segmentation file should contain this pixel value

All elements should be numbered in reading order, unless the format makes that impossible (e.g., elements spanning multiple columns cannot be numbered in reading order because their R value is 254).

Physical layout analysis software may choose to leave some pixels as unclassified; it should follow the following rules:
* if text regions are not marked in their entirety, then the foreground pixels corresponding to characters should have the correct pixel value assigned to them, while all background pixels within the region should be assigned #FFFFFF
* if the layout algorithm detects and uses whitespace layout elements, these should be explicitly indicated using #FFFF80 = (255,255,128) triples in the output

Note that all entities must be numbered consecutively, starting with the value 1 (0 is always reserved).


## Raw Character Segmentation Files

File Names: basename.rseg.png

Low-Level Format: PNG24

These are raw character segments, numbered in reading order from pixel value 1. Groups of adjacend raw segments are considered character candidates. Numbers should be smaller than 4096. Background pixels have the special value 0xffffff. The pixel value 0x000000 is illegal in segmentation files.


## Character Segmentation Files

File Names: basename.cseg.png; transcription in basename.aligned

Low-Level Format: PNG24

Aligned characters. Pixel values start at 1, and the character at position n in basename.aligned (one-based) corresponds to the pixels with value n in the cseg file.


## Lattice Files

File Names: basename.lattice

Recognition output in lattice format

Lattice files consist of two types of lines: “segment” lines and “chr” lines.  The “chr” lines contain recognition results for the preceding segment line.

```
segment 0    1:1    1:1:10:31    20.0000 -0.0000
chr 0       0    0.2162    1
chr 0       1    1.1484    l
segment 1    2:2    13:2:23:31    20.0000 -0.0000
chr 1       0    0.0059    i
segment 2    2:3    13:2:45:31    20.0000 -0.0000
chr 2       0    9.3060    m
chr 2       1    10.4395    rn
```

The “segment” lines have the form:
```
segment <id> <rseg-components-range> <bounding-box> <space-cost> <no-space-cost>
```

The rseg-components-range gives the lowest and highest pixel values of the segmentation components in the corresponding rseg file.  The space costs refer to the log probability of having a space after the current character in the output.  They are returned by the space.model files.

The “chr” lines have the form:
```
chr <segment-id> <chr-id> <cost> <class-in-unicode>
```


## OCR Output

See [ocr-in-html (hOCR)](https://hocr.info)


## External / Other File Formats

Third Party Standards – e.g., the formats used by UW3, XDOC, …



