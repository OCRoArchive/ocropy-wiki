For training ocropy one needs images of lines of text along with [ground truth](https://en.wikipedia.org/wiki/Ground_truth), i.e. the correct transcriptions. Moreover, the ground truth can be used to [estimate the error rate](https://github.com/tmbdev/ocropy/wiki/Compute-errors-and-confusions) resp. the accuracy of the recognition. It is possible to manually generate the ground truth by correcting the recognized text using the command [`ocropus-gtedit`](https://github.com/tmbdev/ocropy/blob/master/ocropus-gtedit).

## File structure

The file and folder structure in `ocropy` follow some fixed rules: Let us assume you have some images of a book which are all saved in one folder. For each page a new subfolder will be created (incremented as four digits number, e.g. `0001`). In such a subfolder, there exists for each line several files: images (png), recognized text (txt), ground truth text (.gt.txt). Not all of the files are present in the beginning.

It is useful to use placeholders like `?` or `*` for calling the commands on several files. For example the term `temp/????/??????.bin.png` will refer to all (binarized) images of lines (incremented by a 6-digits number) on all pages (incremented by a 4-digits number) in the folder temp.

## Correction page

We can create a correction page after we have run `ocropy-rpred`, e.g.
```bash
> ocropus-gtedit html temp/????/??????.bin.png -o temp-correction.html
```
Note that this command already assume that the (binarized) image files as well as the recognized text (txt) are present. See also https://github.com/tmbdev/ocropy/blob/master/run-test for an example in the whole workflow. This correction page can be opened with firefox
```bash
> firefox temp-correction.html &
```

![correction](https://cloud.githubusercontent.com/assets/5199995/11749876/88511cac-a030-11e5-9f41-3193c00e9de1.jpg)

You see the images of all the text lines and below each line there is the recognized text. This input field with the recognized text can be corrected manually to generate the ground truth. For example above you should add the missing letter `I` in the word `REVIEW`. Your result can be saved (as `html` page) again.

## Extract ground truth

Last step is to extract the ground truth, i.e. the correct transcription for each line. This can be done with the command:
```bash
> ocropus-gtedit extract temp-correction.html
```
which will generate all the `.gt.txt`-files.


## All subcommands of `gtedit`

Two of the subcommands of `ocropus-gtedit` are described in the context above. There some more subcommands which can be handy when working with the ground truth. The complete list is:
 * **html**: This generates a html page containing the images
as well as the recognized text, which is useful for manual correction.
Example call: `ocropus-gtedit html temp/????/??????.bin.png -o temp-correction.html`
 * **extract**: This extracts the text out of the html page after the correction
Example call: `ocropus-gtedit extract temp-correction.html`
 * **text**: This creates one text file containing all the information of the single text files which are inputed.
Example call: `ocropus-gtedit text -o gen-text.txt temp/????/??????.txt`
 * **org**: This is the same as text but the file structure is different (org-style).
Example call: `ocropus-gtedit org -o org.txt temp/????/??????.txt`
 * **write**: This writes the text of the individual lines into individual files
in the book directory from the text file containing all text (and the format has to
be as the output of text or org would give it).
Example call: `ocropus-gtedit write -x .test.txt gen-text.txt temp`

Each subcommand has also a help option `-h` where you also see the other possible parameters, e.g. `ocropus-gtedit write -h`.

The structure of the text file or org file looks like the following:

![text](https://cloud.githubusercontent.com/assets/5199995/11909813/0ae0c756-a5ec-11e5-9ef5-09554897fabe.jpg)
![org](https://cloud.githubusercontent.com/assets/5199995/11909777/9fe9edba-a5eb-11e5-8081-da7958ef2368.jpg)



