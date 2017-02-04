The command `ocropus-gpageseg` will segment the page into smaller parts like
columns and lines.

```
ocropus-gpageseg [add here possible options] <input files>
```

As usual, you will find the help for this command by adding `-h` resp. `--help`.

## Input files


## Output

### gray

output grayscale lines as well, default: False

### pad

padding for extracted lines, default: 3

### quiet

be less verbose, default: False

### debug

## Other options

### nocheck

disable error checking on inputs

### zoom

zoom for page background estimation, smaller=faster, default: 0.5

### minscale

minimum scale permitted, default: 12.0

### maxlines

maximum # lines permitted, default: 300

### scale

the basic scale of the document (roughly, xheight) 0=automatic, default: 0.0

### hscale

non-standard scaling of horizontal parameters, default: 1.0

### vscale

non-standard scaling of vertical parameters, default: 1.0

### threshold

baseline threshold, default: 0.2

### noise

noise threshold for removing small components from lines, default: 8

### usegauss

use gaussian instead of uniform, default: False


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


### expand

expand mask for grayscale extraction, default: 3

### parallel

number of CPUs to use

