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
  --gray                output grayscale lines as well, default: False
  -p PAD, --pad PAD     padding for extracted lines, default: 3
  -e EXPAND, --expand EXPAND
                        expand mask for grayscale extraction, default: 3
```

### Binarized and grayscale output

By default only binarized images `.bin.png` of the lines are generated. However,
by adding the parameter `--gray` also normalized grayscale images `.nrm.png`
of all the lines are generated. You can also use grayscale images for training
or prediction, see [FAQ/When can colorful, grayscale or black-and-white images used?](https://github.com/tmbdev/ocropy/wiki/FAQ#when-can-colorful-grayscale-or-black-and-white-images-used) for some
further discussion.

## Line parameters

```
  --threshold THRESHOLD
                        baseline threshold, default: 0.2
  --noise NOISE         noise threshold for removing small components from
                        lines, default: 8
  --usegauss            use gaussian instead of uniform, default: False
```

## Whitespace column separators

It is checked whether any whitespace column separators are present
(by default at most 3) which are important for determining the start and end
of the different lines. For single column text there is no separators and for
two-column text there is exactly one separator in the middle.

```
  --maxcolseps MAXCOLSEPS
                        maximum # whitespace column separators, default: 3
  --csminheight CSMINHEIGHT
                        minimum column height (units=scale), default: 10
```

For example
```
ocropus-gpageseg -d --maxcolseps 0 tests/testpage.png
```
will segment the page into lines without detecting any columns. This results in
long lines which spread across different columns (see the
[debug output](https://cloud.githubusercontent.com/assets/5199995/22626036/491ab17c-eba4-11e6-98f0-c4a4b7ac50a9.png)
). However, by calling
```
ocropus-gpageseg -d --maxcolseps 1 tests/testpage.png
```
the lines are separated among the two columns, because the white space
separator in the middle was found and taken into account (see the
[debug output](https://cloud.githubusercontent.com/assets/5199995/22626037/4c1ff472-eba4-11e6-958b-b38e8ece17d1.png)
).


## Black column separators

By default, the black column separators are not checked, but this can be
changed by setting the `maxseps` parameter to a positive number:

```
  --maxseps MAXSEPS     maximum black column separators, default: 0
  --sepwiden SEPWIDEN   widen black separators (to account for warping),
                        default: 10
```


## Check

```
  -n, --nocheck         disable error checking on inputs
  --minscale MINSCALE   minimum scale permitted, default: 12.0
  --maxlines MAXLINES   maximum # lines permitted, default: 300
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
