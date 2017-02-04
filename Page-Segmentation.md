🚧 _Work in Progress_ 🚧  
_Help us by extending this notes..._

---

The command `ocropus-gpageseg` will segment the page into smaller parts like
columns and lines.

```
ocropus-gpageseg [add here possible options] <input files>
```


## Input files

For input, you can name one or several `png` images, which usually you will
be given after the `ocropus-nlbin` command. For each file name a binarized
version with the file ending `.bin.png` is looked for and the computation
here is actually done on this binarized image. For some option you also
need a normalized grayscale image with the file ending `.nrm.png`.

For example all of these calls
```
ocropus-gpageseg test
ocropus-gpageseg test.png
ocropus-gpageseg test.bin.png
```
will make the computation on `test.bin.png` (if this does not exists then
an error is thrown).


## Output

For each input image a new folder with this base name is
created and inside this folder the images of all detected
lines are saved. They are named with 6 hexadecimal digits
starting from `010000`.

Moreover, a `pseg.png` file is created, [OCRopus-File-Formats/Physical Layout](https://github.com/tmbdev/ocropy/wiki/OCRopus-File-Formats#physical-layout) for more details.

```
  --gray                output grayscale lines as well, default: False
  -p PAD, --pad PAD     padding for extracted lines, default: 3
  -e EXPAND, --expand EXPAND
                        expand mask for grayscale extraction, default: 3
```


## line parameters

```
  --threshold THRESHOLD
                        baseline threshold, default: 0.2
  --noise NOISE         noise threshold for removing small components from
                        lines, default: 8
  --usegauss            use gaussian instead of uniform, default: False
```


### Black column separators

```
  -- maxseps MAXSEPS      maximum black column separators, default: 2
  --sepwiden SEPWIDEN   widen black separators (to account for warping),
                        default: 10
  -b, --blackseps       also check for black column separators
```


### whitspace column separators

```
  --maxcolseps MAXCOLSEPS
                        maximum # whitespace column separators, default: 2
  --csminaspect CSMINASPECT
                        minimum aspect ratio for column separators
  --csminheight CSMINHEIGHT
                        minimum column height (units=scale), default: 10
```


## Check, scale, zoom

```
  -n, --nocheck         disable error checking on inputs
  -z ZOOM, --zoom ZOOM  zoom for page background estimation, smaller=faster,
                        default: 0.5
  --minscale MINSCALE   minimum scale permitted, default: 12.0
  --maxlines MAXLINES   maximum # lines permitted, default: 300
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