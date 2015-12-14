For training ocropy one needs images of lines of text along with [ground truth](https://en.wikipedia.org/wiki/Ground_truth), i.e. the correct transcriptions. Moreover, the ground truth can be used to estimate the error rate resp. the accuracy of the recognition. It is possible to manually generate the ground truth by correcting the recognized text using the command [`ocropus-gtedit`](https://github.com/tmbdev/ocropy/blob/master/ocropus-gtedit).

## File structure

The file and folder structure in `ocropy` follow some fixed rules: Let us assume you have some images of a book which are all saved in one folder. For each page a new subfolder will be created (incremented as four digits number, e.g. `0001`). In such a subfolder, there exists for each line several files: images (png), recognized text (txt), ground truth text (.gt.txt). Not all of the files are present in the beginning.

It is useful to use placeholders like `?` or `*` for calling the commands on several files. For example the term `temp/????/??????.bin.png` will refer to all (binarized) images of lines (incremented by a 6-digits number) on all pages (incremented by a 4-digits number) in the folder temp.

## Correction page

We can create a correction page after we have run `ocropy-rpred`, e.g.
```
> ocropus-gtedit html temp/????/??????.bin.png -o temp-correction.html
```
Note that this command already assume that the (binarized) image files as well as the recognized text (txt) are present. See also https://github.com/tmbdev/ocropy/blob/master/run-test for an example in the whole workflow. This correction page can be opened with firefox
```
> firefox temp-correction.html &
```

![correction](https://cloud.githubusercontent.com/assets/5199995/11749876/88511cac-a030-11e5-9f41-3193c00e9de1.jpg)

You see the images of all the text lines and below each line there is the recognized text. This input field with the recognized text can be corrected manually to generate the ground truth. For example above you should add the missing letter `I` in the word `REVIEW`. Your result can be saved (as `html` page) again.

## Extract ground truth

Last step is to extract the ground truth, i.e. the correct transcription for each line. This can be done with the command:
```
> ocropus-gtedit extract temp-correction.html
```
which will generate all the `.gt.txt`-files.