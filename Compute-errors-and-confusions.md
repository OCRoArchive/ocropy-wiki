After the recognition and manually [generating the ground truth](https://github.com/tmbdev/ocropy/wiki/Working-with-Ground-Truth) for some lines/pages, it is possible to compute the errors for these lines. There is the command `ocropus-errs` for computing the errors and `ocropus-econf` for computing the confusions.

## How to count errors?

The [edit distance](https://en.wikipedia.org/wiki/Edit_distance) will be computed between the ground truth and the recognizer output. Thus, one error could mean that a character is missing, a character should be deleted, or that a character should be changed to another character. If we have to change a single character with two other characters (or the other way around) this would have edit distance two.

**Example**
```
RECOGNIZER:     la cupidire, 8c divers interêts
GROUND TRUTH:   la cupidité, & divers interêts
                         ^^  ^^               
```
This two lines have edit distance 4 and we would get two confusions `re -> té`, `8c -> &`

## Prerequisites

We need to have a set of lines for which we have the recognized text together with the ground truth of these lines. The corresponding lines must have the same name but different file ending. The files should lie in the same directory.

## Computations

The commands `ocropus-errs` and `ocropus-econf` need the ground truth files of the lines as an argument, e.g.
```bash
> ocropus-errs *.gt.txt

errors          14 
missing          0 
total         2555 
err          0.548 % 
Errnomiss    0.548 %
```
resp.
```bash
> ocropus-econf *.gt.txt

1	_	-
1	W	w
1	H_	fi
1	!	_
1	_____	that 
1	H_	fl
1	e	_
1	_	'
```

There are several optional arguments to these two commands. The most important are:
```
  -x EXTENSION, --extension EXTENSION
                        extension for recognizer output, default: .txt
  -k KIND, --kind KIND  kind of comparison (exact, nospace, letdig, letters,
                        digits, lnc), default: exact
  -s, --skipmissing     don't use missing or empty output files in the
                        calculation
```


