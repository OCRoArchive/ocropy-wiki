## How to install Ocropus on a Mac?

Starting from version 1.3.3 the default installation should exactly the
same. Previously, there was some native C code which was needed to compile
dynamically with a compiler with a different flag for Mac.

## How to install Ocropus on Windows?

https://github.com/tmbdev/ocropy/issues/73 and 
https://github.com/tmbdev/ocropy/issues/263#issuecomment-347008893

## How to install Ocropus on Fedora?

https://github.com/tmbdev/ocropy/issues/48

## How to install Ocropus on Linux Mint?

https://github.com/tmbdev/ocropy/issues/191

## How to install Ocropus on CentOS?

https://github.com/tmbdev/ocropy/issues/226

## Is there a docker image for Ocropus?

Yes, e.g. https://hub.docker.com/r/kbai/ocropy/

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


## What exactly is meant by 300 dpi for digital images?

The default parameters and settings of OCRopus assume 300dpi scanned images with black text on white pages and some standard font size (9pt to 14pt).
This is normally the first thing you should check when the recognition quality is not good.
When using a document/book scanner you normally can adjust this parameter, with other devices like a fax or smartphone camera you might not have this information.

As an indication: An A4-papier (210mm × 297mm) scanned with 300dpi results in an image with 2504 x 3540 pixels.

Pictures with low resolution or very hight resolution (e.g. 1200dpi) will usually not work well (there are some tests which might alerting the user in these cases).
Resizing/rescaling the image might help in cases you can influence the scan quality on the device itself. Possible algorithms for that are:
* ImageMagick's `convert`
* People have reported good results with [Waifu2x](http://waifu2x.udp.jp/)
* [neural-enhance](https://github.com/alexjc/neural-enhance)


## What is the "ALN" line during training?

ALN is the result of decoding the alignment of the raw output with the ground truth. That is, ALN uses the ground truth. You can't use it for predictions, but it helps follow the progress of training.

## How to avoid the UserWarning: Matplotlib is building the font cache?

If you see in the beginning of the commands the following warning
```
/usr/lib/python2.7/dist-packages/matplotlib/font_manager.py:273: UserWarning: Matplotlib is building the font cache using fc-list. This may take a moment.
  warnings.warn('Matplotlib is building the font cache using fc-list. This may take a moment.')
```
then one of or several of the following calls should help
```
rm -rf ~/.matplotlib
rm -rf ~/.cache/matplotlib
rm -rf ~/.cache/fontconfig/
```

See https://github.com/matplotlib/matplotlib/issues/5836

## How can Ocropus be run on a command line only without graphical output?

Try to set `export MPLBACKEND="agg"`.