This is a list of trained models for recognition with ocropy. 

Download the models and copy them to one of:
* `$OCROPUS_DATA`, which you can define in the environment, e.g. in `~/.bashrc`: `OCROPUS_DATA=/data/ocropus-models/`
* the working directory where you run `ocropus-*`
* a subdirectory `./models` from the current working directory
* `/usr/local/share/ocropus`
* `/usr/share/ocropus`

## Latin Scripts
 * English Default: http://www.tmbdev.net/en-default.pyrnn.gz (80 MB)
 * Fraktur: http://tmbdev.net/ocropy/fraktur.pyrnn.gz (42 MB)
 * Fraktur: https://github.com/jze/ocropus-model_fraktur (including training data and a model for [CLSTM](https://github.com/tmbdev/clstm))
 * early 20th century antiqua including south-east European characters: https://github.com/jze/ocropus-model_oesterreich-ungarn (including training data)
 * (Old) French: https://github.com/zuphilip/ocropy-french-models (26 MB)
 * [Older models by @tmbdev: http://www.tmbdev.net/ocropy/OLD/]
 * models (normal text, italics) trained with the Hume Dialogues text (English text, published 1779): https://github.com/urhub/ocropy/tree/master/models
 * a mixed OCRopus model trained on twelve Latin books printed with Antiqua types between 1471 and 1686 with a focus (ten out of twelve) on early works produced before 1600: https://github.com/chreul/OCR_Testdata_EarlyPrintedBooks (16MB)


## Polytonic Greek Script
 * https://github.com/brobertson/ciaconna/tree/master/Classifiers

## Cyrillic Scripts
 * https://github.com/jze/ocropus-model_cyrillic

## Asian Scripts
 * Japanese by @isaomatsunami: https://github.com/isaomatsunami/clstm-Japanese (56 MB)

## Indic Scripts
 * Telugu model & training data: https://github.com/ChillarAnand/likitham

## Coptic
 * Coptic models: https://github.com/KELLIA/CopticOCR/tree/master
