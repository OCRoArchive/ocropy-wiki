# Older versions of ocropus

## LSTM-based versions
### LSTM-based OCR engine only
* [OCRopy v1.3.3](https://github.com/tmbdev/ocropy/releases/tag/v1.3.3) released 2017-12-16
* [OCRopy v1.3.2](https://github.com/tmbdev/ocropy/releases/tag/v1.3.2) released 2017-12-16
* [OCRopy v1.3.1](https://github.com/tmbdev/ocropy/releases/tag/v1.3.1) released 2017-10-17
* [OCRopy v1.3.0](https://github.com/tmbdev/ocropy/releases/tag/v1.3.0) released 2017-08-11
* [OCRopy v1.2.0](https://github.com/tmbdev/ocropy/releases/tag/v1.2.0) released 2016-12-04
* [OCRopy v1.1.1](https://github.com/tmbdev/ocropy/releases/tag/v1.1.1) released 2016-01-28
* [OCRopy v1.1.0](https://github.com/tmbdev/ocropy/releases/tag/v1.1.0) released 2015-04-24
* [OCRopy v1.0](https://github.com/tmbdev/ocropy/releases/tag/v1.0) released 2014-11-02

### LSTM-based OCR engine and the OCR engine from v0.6
* [v0.8.1 classic-ocropy-0.1.1](https://github.com/tmbdev/ocropy/releases/tag/v0.8.1) released 2014-11-01
* [v0.8.0 classic-ocropy-0.1](https://github.com/tmbdev/ocropy/releases/tag/v0.8.0) 2013-09-05
* [v0.7](https://github.com/tmbdev/ocropy/releases/tag/v0.7) 2013-04-06 [a79c658](https://github.com/tmbdev/ocropy/commit/a79c6581171a63d5adffeaf8692d6b550b74bff5)
    * a new text line recognizer based on recurrent neural networks (and does not require language modeling)
    * models for both Latin script and Fraktur
    * new tools for ground truth labeling
    * Text line recognition error rates are much lower than with previous systems, in many cases beating commercial systems in benchmarks on standard databases. Training for new scripts has also been simplified greatly.
    * Source: [message in the discussion group](https://groups.google.com/forum/#!msg/ocropus/Jpqz_Kc9M8g/y1uIZQTwfbQJ)

See also [https://github.com/tmbdev/ocropy/releases](https://github.com/tmbdev/ocropy/releases).

## Older versions
In the old days there was a main 'ocropus' repository with references to 'ocropy' and other sub-repos. The versions were attached to the main repository, but we have now retro-perspectively added these version numbers also to the ocropy repository to corresponding commits of the same time.
### ocropy repository
* [v0.6](https://github.com/tmbdev/ocropy/releases/tag/v0.6) 2012-08-23 [820f513](https://github.com/tmbdev/ocropy/tree/820f513f8b987a)
    * Major changes relative to 0.5.x are much simpler installation, fewer dependencies, better character recognition rates, and easier training.  There is also a number of sample scripts illustrating recognition and training.
    * Source: [message in the discussion group](https://groups.google.com/forum/#!msg/ocropus/L-BJyrPcTYM/784w6OSv3fMJ)
* [v0.5.4](https://github.com/tmbdev/ocropy/releases/tag/v0.5.4) 2012-07-15 [092c5d0](https://github.com/tmbdev/ocropy/tree/092c5d081163)
* [v0.5.3](https://github.com/tmbdev/ocropy/releases/tag/v0.5.3) 2012-07-15 [faec00d](https://github.com/tmbdev/ocropy/commit/faec00de3fb46984443dda641e6244d6881bd50f)
* [v0.5.2](https://github.com/tmbdev/ocropy/releases/tag/v0.5.2) 2012-07-15 [107b198](https://github.com/tmbdev/ocropy/commit/107b1983324bb29a62348912c3fe471f42d0bbc1)
* [v0.5.1](https://github.com/tmbdev/ocropy/releases/tag/v0.5.1) 2012-05-11 [81741ba](https://github.com/tmbdev/ocropy/commit/81741ba1231d157f49823cde6252fffdf6d18c29)
* [v0.5](https://github.com/tmbdev/ocropy/releases/tag/v0.5) 2012-03-06 [92db6f5](https://github.com/tmbdev/ocropy/tree/92db6f51bbe6)
   * OCRopus has been completely refactored and now consists of a set of Python modules, with some native code modules.
   * Unicode and ligature support should be fully working now.
   * Language modeling still uses finite state transducers, but all finite state transducer code has been refactored into ocrofst.
   * There is a completely new recognizer that performs much better than the old recognizer and scales to millions of training samples.
   * Databases for training/testing have been changed from SQLite format to HDF5 (using PyTables).
   * Source: [message in the discussion group](https://groups.google.com/forum/#!topic/ocropus/S73OMtJdVmw/discussion)
* [first commit in the ocropy repo](https://github.com/tmbdev/ocropy/commit/ec43558af20a) 2010-03-03

### ocropus repository
* [v0.?](https://github.com/zuphilip/ocropus-from-searchcode) 2012?-??-??
* [v0.4.4](https://github.com/michaelyin/ocropus-git/tree/ba6930627f3f) 2010-03-24
    * all recognition can now be carried out from Python
    * there are top-level commands for recognition and training written in Python
    * classifiers now can cope with large character sets
    * there are tools for clustering and correcting character shapes
    * there is support for ligatures
    * there are numerous bug fixes
    * training is possible on very large datasets (many millions of samples) 
* _v0.4.3_ 2009-07
    * new book storage format
    * basic dynamic loading support
    * added sample extension to repository
    * bug fixes 
* _v0.4.2_
   * (0.4.2 didn't pass testing, so it's not recommended.) 
* _v0.4.1_ 2009-07
    * rewritten string classes (ustrg, strg, utf8strg) in preparation for better Unicode support
    * IBookStore and OldBookStore abstractions for book directory access
    * disabled OpenMP by default
    * multipage TIFF support
    * bug fixes     rewritten string classes (ustrg, strg, utf8strg) in preparation for better Unicode support
    * IBookStore and OldBookStore abstractions for book directory access
    * disabled OpenMP by default
    * multipage TIFF support
    * bug fixes 
* [v0.4](https://github.com/michaelyin/ocropus-git/tree/4ab75dc0dc9b) 2009-05-31 "Alpha 4":
    * This is essentially the functionality in the Mercurial repository at mercurial.iupr.org
        * OCRopus has been turned into a library
        * there is a new set of command line programs for book-level recognition
        * there is a new line recognizer
        * there is a new component model
        * OCRopus supports book-level retraining and adaptation
        * there are new preprocessing functions
        * there is a new language modeling system
        * there are many improvements to layout analysis
        * OpenFST support is now optional
        * there is TIFF support
        * Lua support has been factored into a separate repository (ocroscript)
        * there is a separate, new Python binding 
    * Some limitations:
        * autoconf/automake has not been tested much
        * the character shape models use a simple model and have been trained on only about 1.5M characters
            * performance will be worse than 0.3 on some documents (and better on others)
            * you can get the 0.3 recognizer as part of a separate ocrotess component
            * for 0.5 (beta) we expect to have much larger models trained and in place 
        * the language model is a simple combination of a dictionary, some case rules
            * for 0.5 (beta) we expect to have much better language models 
        * the recognizer still has a lot of rough edges 
    * Note that you will probably encounter some exceptions or error messages while running OCRopus. That's usually harmless: those exceptions indicate real error conditions, but they are usually handled in some sensible way. For example, the layout analysis may sometimes pass a (non-text) image to the line recognizer, and the line recognizer will probably raise an exception. 
* [v0.3](https://github.com/michaelyin/ocropus-git/tree/d39c2e3) 2008-10-15 "Alpha 3":
    * image understanding related code is now in a separate project (www.iulib.org)
    * move to autoconf/automake build system
    * support for beam search decoding (OpenFST is now optional)
    * fixed memory leaks in Voronoi page segmentation code
    * ported Voronoi page segmentation code to 64-bit architecture
    * word segmentation
    * refactored text/image segmentation code
    * optional access to text/image segmentation from Leptonica
    * inclusion of images and other non-text zones in the hOCR output
    * optional inclusion of character boxes in the hOCR output
    * improved edit distance with block movement for OCR evaluation
    * scripts for evaluation of Layout and OCR performance
    * bug fixes in bpnet (normalization of input data, right loading of a bpnet)
    * feature selection, feature size selection, fix bug in skeleton feature, added connected component segmenter for train and test
    * scripts for training/testing bpnet, documentation
    * better loggers for training and testing (confusion matrix, lineinfo, segmenter, fst, etc)
    * more accurate text line analysis 
* _v0.2_ 2008-05-30 "Alpha 2":
    * fixed dependency problems in jam
    * implement OCR output in lua (in particular, hOCR output routines)
    * reduced memory usage of layout analysis
    * xy-cut layout analysis
    * Voronoi-based layout analysis (donated by K. Kise)
    * Otsu binarization (in addition to our own fast Sauvola)
    * script-based automatic EM training
    * OCRopus and libraries callable directly from Python/NumPy
    * replacement of ocrocmd by customizable Lua-scripts
    * new beam search decoder
    * graphical logging and debugging facility
    * various bug fixes
    * more Documentation 
* _v0.1.1_ 2007-12-14: "This is the first maintenance release of OCRopus Alpha, which introduces closer cooperation with Tesseract to improve speed and accuracy. It also fixes several portability issues."
    * This is a minor bug-fix release. 
* _v0.1.0_ 2007-10-22: "The first packaged release aims to stabilize the interfaces of the involved components and provides a first version of the scripting functionality for OCRopus based on Lua. It also includes some more preprocessing functionality for document images and a MLP based character classifier."
    * The alpha release (OCRopus 0.1.0) is the first numbered release of OCRopus. Its purpose has been to get the major code organization and interfaces in place so that people can start building add-ons for OCRopus. There's a lot of functionality relative to the pre-alpha six months ago:
        * text/image segmentation
        * MLP-based character recognition
        * OpenFST-based statistical language modeling
        * more detailed layout information in the hOCR output
        * better testing and evaluation tools
        * some image cleanup, deskewing
        * Lua-based configuration and scripting
        * fast binary morphology
        * better code organization through namespaces, include file simplifications
        * code for alignment and training data generation from transcribed ground truth 
    * You can use this an open source OCR system, by using OCRopus with Tesseract (this gives you about Tesseract's per-character error rates with OCRopus layout analysis and preprocessing.
    * More importantly, if you're working on your own layout analysis, character recognition, or language modeling, this is a release that you can start developing plug-ins or add-ons for, since we're going to try to keep these interfaces stable. 
* [Announcing the OCRopus Open Source OCR System](https://developers.googleblog.com/2007/04/announcing-ocropus-open-source-ocr.html) April 9, 2007 and remark in old [CHANGES](https://github.com/michaelyin/ocropus-git/blob/d39c2e396b2afa700932a0523d06bc4a246a2ec2/CHANGES): "The Ocropus svn was opened to the public in April 2007 in order to give a first preview of the project. The Technology Preview internally combined Tesseract 1.x with some Layout Analysis algorithms. In this stage, a basic system was already working but the whole architecture was still changing as well as the interfaces for the respective modules / components."