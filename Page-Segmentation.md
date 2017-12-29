_Work in Progress_
_Help us by extending these notes..._

---

The command [`ocropus-gpageseg`](https://github.com/tmbdev/ocropy/blob/master/ocropus-gpageseg)
will segment the page into smaller parts like columns and lines.

```
ocropus-gpageseg [add here possible options] <input files>
```


## Input files

For input, you can name one or several `png` images, which usually you will
be given after the `ocropus-nlbin` command. For each file name a binarized
version with the file ending `.bin.png` is looked for and the computation
here is actually done on this binarized image. (However, it is still important
that the file name points to an existing file.)

For example all of these calls
```
ocropus-gpageseg test.jpg
ocropus-gpageseg test.bin.png
ocropus-gpageseg test.nrm.png
```
will make the computation on `test.bin.png` (if this does not exists then
an error is thrown).


## Output

For each input image a new folder with this base name is
created and inside this folder the images of all detected
lines are saved. They are named with 6 hexadecimal digits
starting from `010000`.

Moreover, a `pseg.png` file is created, [OCRopus-File-Formats/Physical Layout](https://github.com/tmbdev/ocropy/wiki/OCRopus-File-Formats#physical-layout) for more details.

The following parameters influence the output further:


```
  --noise NOISE         noise threshold for removing small components from
                        lines, default: 8
  -p PAD, --pad PAD     padding for extracted lines, default: 3
  --gray                output grayscale lines as well, default: False
  -e EXPAND, --expand EXPAND
                        expand mask for grayscale extraction, default: 3
```

### Noise removal

There is a step which removes small components from the whole image just before outputing the individual lines. These small components are usually just some noise and should be considerable smaller than for example the period as a punctation mark or the point in the `i`:

<img src="https://user-images.githubusercontent.com/5199995/34437728-2c4f2dda-eca1-11e7-8456-c3e10deddbf6.png" width=300px/> -- noise removal -->
<img src="https://user-images.githubusercontent.com/5199995/34437732-30c30bde-eca1-11e7-8793-9b6193b58366.png" width=300px/>

In the noise removal step only components of size at most 8 are remove by default. This threshold can be adjusted by the parameter `--noise NOISE`. For example `--noise 30` will remove also components of size at most 30 (containing most `.` and points in `i` for the example) and `--noise 0` will deactivate the noise removal completely.


### Binarized and grayscale output

By default only binarized images `.bin.png` of the lines are generated. However,
by adding the parameter `--gray` also normalized grayscale images `.nrm.png`
of all the lines are generated. You can also use grayscale images for training
or prediction, see [FAQ/When can colorful, grayscale or black-and-white images used?](https://github.com/tmbdev/ocropy/wiki/FAQ#when-can-colorful-grayscale-or-black-and-white-images-used) for some
further discussion.

🚧 What does `--expand EXPAND` exactly? 🚧 

### Padding

The outputed line images have an additional white space around the actual text (on the top, left bottom and right). The amount of space is determined by the padding value `--pad PAD` which is set by default to `3` pixels. If you want more spacing around the actual text lines, then provide higher padding value. If you don't want any padding, then use `--pad 0`.


## Line parameters

```
  --threshold THRESHOLD
                        baseline threshold, default: 0.2
  --usegauss            use gaussian instead of uniform, default: False
```

## Column separators

It is checked whether any _whitespace column separators_ are present
(by default at most 3) which are important for determining the start and end
of the different lines. For single column text there is no separators and for
two-column text there is exactly one separator in the middle.

```
  --maxcolseps MAXCOLSEPS
                        maximum # whitespace column separators, default: 3
  --csminheight CSMINHEIGHT
                        minimum column height (units=scale), default: 10
```


By default, the _black column separators_ are not checked, but this can be
changed by setting the `maxseps` parameter to a positive number:

```
  --maxseps MAXSEPS     maximum black column separators, default: 0
  --sepwiden SEPWIDEN   widen black separators (to account for warping),
                        default: 10
```

### Example for column separators

```
ocropus-gpageseg -d --maxcolseps 0 tests/testpage.png
```
will segment the page into lines without detecting any columns. This results in
long lines which spread across different columns:

![debug output](https://cloud.githubusercontent.com/assets/5199995/22626036/491ab17c-eba4-11e6-98f0-c4a4b7ac50a9.png)

However, by calling
```
ocropus-gpageseg -d --maxcolseps 1 tests/testpage.png
```
the lines are separated among the two columns, because the white space
separator in the middle was found and taken into account:

![debug output](https://cloud.githubusercontent.com/assets/5199995/22626037/4c1ff472-eba4-11e6-958b-b38e8ece17d1.png)

The column separators are bounds for the following line detection. However, note that the "smearing" does stop at some point. Therefore, there are even different lines detected, when there is no column separator at all. For example the footer in the previous pictures will be put into two lines with both parameters. 

## Consistency checks

There are some consistency checks during the page segmentation. If any of these checks finds an unusual value, then the computation is stopt and an error message is shown. The standard check tries to make sure that the image has a reasonable size and is binarized; moreover, there are checks to make sure that the scale is not too small and the maximum number of lines is not too high. These checks and values can be controlled by these parameters:

```
  -n, --nocheck         disable error checking on inputs
  --minscale MINSCALE   minimum scale permitted, default: 12.0
  --maxlines MAXLINES   maximum # lines permitted, default: 300
```

The default values should work fine for an usual A4 paper of an article or book page with 300 dpi. However, the might not work well for very small images or newspaper pages with a lot of text lines. In such cases it might be necessary to deactivate the check and/or adjust the values, e.g.

```
ocropus-gpageseg -n --minscale 5 --maxlines 900 tests/testpage.png
```

## Scale

```
  --scale SCALE         the basic scale of the document (roughly, xheight)
                        0=automatic, default: 0.0
  --hscale HSCALE       non-standard scaling of horizontal parameters,
                        default: 1.0
  --vscale VSCALE       non-standard scaling of vertical parameters, default:
                        1.0
```


## Other options

```
  -q, --quiet           be less verbose, default: False
  -d, --debug
  -h, --help            show this help message and exit
  -Q PARALLEL, --parallel PARALLEL
                        number of CPUs to use
```
