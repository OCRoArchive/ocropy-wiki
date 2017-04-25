_Work in Progress_
_Help us by extending these notes..._

---

The command [`ocropus-rpred`](https://github.com/tmbdev/ocropy/blob/master/ocropus-rpred) will recognize the text from images of single lines with a RNN.
```
ocropus-rpred [add here possible options] <input files>
```

## Input Files

## Models

## Recognition

```
  -m MODEL, --model MODEL
                        line recognition model
  -p PAD, --pad PAD     extra blank padding to the left and right of text line
  -N, --nonormalize     don't normalize the textual output from the recognizer
  --llocs               output LSTM locations for characters
  --alocs               output aligned LSTM locations for characters
  --probabilities       output probabilities for each letter
```

## Line normalization (dewarping)

By default a [line normalizer](https://github.com/tmbdev/ocropy/blob/master/ocrolib/lineest.py) is used to dewarp the single lines before the actual recognition:

![before-dewarp](https://cloud.githubusercontent.com/assets/5199995/25391160/e28caec2-29d5-11e7-9f58-bb1606358064.png)
![after-dewarp](https://cloud.githubusercontent.com/assets/5199995/25391318/4961024c-29d6-11e7-8b3f-d131c1c09e3e.png)

The dewarping of the text line (first image) tries to find the center (blue curve) and then cut out slices with some fixed radius around the center (cf. [this illustration](https://cloud.githubusercontent.com/assets/5199995/25392360/bcadf60e-29d8-11e7-9ed7-acfba811f8a4.png)). This will then assure that the center line is horizontally and thereby the text line dewarped.

The default behavior can be influence by these two parameters:
```
  -e, --nolineest       deactivate the text normalizer and therefore the dewarping
  -l HEIGHT, --height HEIGHT
                        overrides the target line height, which is 48
```

These parameters make only sense if the model is also trained under the same conditions and usually there is no need to use them at all.

## Error Measures

```
  -r, --estrate         estimate error rate only
  -c ESTCONF, --estconf ESTCONF
                        estimate confusion matrix
  -C COMPARE, --compare COMPARE
                        string comparison used for error rate estimate
  --context CONTEXT     context for error reporting
```

## Debugging, Help

```
  -s SHOW, --show SHOW  if >0, shows recognition output in a window and waits
                        this many seconds
  -S SAVE, --save SAVE  save debugging output image as PNG (for bug reporting)
  -h, --help            show this help message and exit
  -n, --nocheck         disable error checking on inputs
  -q, --quiet           turn off most output
  -Q PARALLEL, --parallel PARALLEL
                        number of parallel processes to use, default: 1
```
