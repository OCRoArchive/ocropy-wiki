## How to install Ocropus on a Mac?

https://github.com/tmbdev/ocropy/blob/master/README_OSX.md

## How to install Ocropus on windows?

https://github.com/tmbdev/ocropy/issues/73

## When can colorful, grayscale or black-and-white images used?

 * Binarization `ocropus-nlbin`: You can input colorful pictures and the output are a binarized black-white version `.bin.png` as well as a grayscale version `.nrm.png`.
 * Page Segmentation `ocropus-gpageseg`: You can input a grayscale or black-and-white picture (any colorful picture will be automatically transformed to a grayscale picture). The output are by default black-and-white lines, but with the option `--gray` it is possible to output also grayscale lines.
 * Text recognition `ocropus-rpred`: You can use either the binarized lines `.bin.png` or the grayscale lines `.nrm.png`. 
 * Training `ocropus-rtrain`: You can use either the binarized lines `.bin.png` or the grayscale lines `.nrm.png`.

_Tips on the usage:_ `ocropus-rtrain` was intended to be used with grayscale, but `ocropus-rpred` was not. Grayscale images can be especially useful in cases where binarization leads to a loss of connectedness in glyph shapes.