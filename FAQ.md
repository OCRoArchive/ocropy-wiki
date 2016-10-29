## How to install Ocropus on a Mac?

https://github.com/tmbdev/ocropy/blob/master/README_OSX.md

## How to install Ocropus on windows?

https://github.com/tmbdev/ocropy/issues/73

## When can colorful, grayscale or black-and-white images used?

 * Binarization `ocropus-nlbin`: You can input colorful pictures and the output are a binarized black-white version `.bin.png` as well as a grayscale version `.nrm.png`.
 * Page Segmentation `ocropus-gpageseg`: You can input a (normalized) grayscale or black-and-white picture (any colorful picture will be automatically transformed to a grayscale picture). The output are by default black-and-white lines, but with the option `--gray` it is possible to output also normalized grayscale lines.
 * Text recognition `ocropus-rpred`: You can use either the binarized lines `.bin.png` or the (normalized) grayscale lines `.nrm.png`. 
 * Training `ocropus-rtrain`: You can use either the binarized lines `.bin.png` or the (normalized) grayscale lines `.nrm.png`.

_Tips on the usage:_ `ocropus-rtrain` was intended to be used with grayscale, but `ocropus-rpred` was not. Grayscale images can be especially useful in cases where binarization leads to a loss of connectedness in glyph shapes. Ocropus preprocessing will generate normalized grayscale images, that's what you should use. If you just cut out grayscale images yourself, it probably won't work as well.

Generally, in order to get good performance out of the 1D LSTM, you need line normalization. The line normalizer requires binary input. So, there are different options: you can run both recognition and normalization with binary input (which is used for both normalization and recognition), you can supply a grayscale image and the library will generate a binary image for normalization, or you can supply both a grayscale and a binary input, in which case the binary input is used for normalization and the grayscale for recognition. At least that was the original idea; most of the applications have used binary only, so the other codepaths haven't been tested much. Furthermore, "grayscale" usually means "normalized grayscale", that is, something that looks nearly binary but may have gray pixels around the edges