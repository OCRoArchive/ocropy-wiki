## How to install Ocropus on a Mac?

https://github.com/tmbdev/ocropy/blob/master/README_OSX.md

(related issue [#70](https://github.com/tmbdev/ocropy/issues/70))

## How to install Ocropus on windows?

https://github.com/tmbdev/ocropy/issues/73

## How to install Ocropus on fedora?

https://github.com/tmbdev/ocropy/issues/48

## How to install Ocropus on Linux Mint?

https://github.com/tmbdev/ocropy/issues/191

## When can colorful, grayscale or black-and-white images used?

 * Binarization `ocropus-nlbin`: You can input colorful pictures and the output are a binarized black-white version `.bin.png` as well as a grayscale version `.nrm.png`.
 * Page Segmentation `ocropus-gpageseg`: You can input a (normalized) grayscale or black-and-white picture (any colorful picture will be automatically transformed to a grayscale picture). The output are by default black-and-white lines, but with the option `--gray` it is possible to output also normalized grayscale lines.
 * Text recognition `ocropus-rpred`: You can use either the binarized lines `.bin.png` or the (normalized) grayscale lines `.nrm.png`. 
 * Training `ocropus-rtrain`: You can use either the binarized lines `.bin.png` or the (normalized) grayscale lines `.nrm.png`.

_Tips on the usage:_ `ocropus-rtrain` was intended to be used with grayscale, but `ocropus-rpred` was not. Grayscale images can be especially useful in cases where binarization leads to a loss of connectedness in glyph shapes. Ocropus preprocessing will generate normalized grayscale images, that's what you should use. If you just cut out grayscale images yourself, it probably won't work as well.

Generally, in order to get good performance out of the 1D LSTM, you need line normalization. The line normalizer requires binary input. So, there are different options: you can run both recognition and normalization with binary input (which is used for both normalization and recognition), you can supply a grayscale image and the library will generate a binary image for normalization, or you can supply both a grayscale and a binary input, in which case the binary input is used for normalization and the grayscale for recognition. At least that was the original idea; most of the applications have used binary only, so the other codepaths haven't been tested much. Furthermore, "grayscale" usually means "normalized grayscale", that is, something that looks nearly binary but may have gray pixels around the edges

## Should I use scans of single pages or can I also use scans of two pages in the same image?

It is possible to use scans of two pages in the same image, which will then be handled equivalent as one page with two columns. This can work okay if the scan is good and equivalent (no different skewing, enough space around the joint/fold). However, in most cases it is better to split the double-page into two single page images before continue with the OCR. For doing this task one can use for example:
* Imagemagick `convert` function with crop (described in [this blog article](http://hdw.artsci.wustl.edu/articles/154)):
```
for i in *.tif; do echo $i; convert $i -crop 2x1+0+0@ +repage +adjoin [insert_output_folder_name_here]/output$i; done
```
* ScanTailor: http://scantailor.org/
* unpaper: https://github.com/Flameeyes/unpaper


## Can ocropus be used for handwritten text recognition?

Well, in theory this should work, but probably need a lot of training data (images + ground truth) and training steps. I don't know of anyone has done much into this direction with ocropus. There might be other software/projects more tailored for handwritten text, e.g. https://transkribus.eu/Transkribus/ .


## What is the "ALN" line during training?

ALN is the result of decoding the alignment of the raw output with the ground truth. That is, ALN uses the ground truth. You can't use it for predictions, but it helps follow the progress of training.
