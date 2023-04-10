## Ideas for further development of Tesseract

### Conversion of neural networks for text recognition to and from Tesseract

As long as the networks are compatible with the features implemented in Tesseract, it should be possible to convert models made for Keras or Tensorflow to Tesseract and vice versa.

Maybe ONXX can be used as a common exchange format:

- https://github.com/onnx/onnx/blob/master/docs/ImplementingAnOnnxBackend.md

Related issues:

- [Use Tesseract models for Kraken](https://github.com/mittagessen/kraken/issues/152) (requires conversion from Tesseract to Keras)

### Support additional image formats

Tesseract uses Leptonica which can read many important image formats. Releant Leptonica API functions: `pixRead`, more?

Missing formats:

* [AVIF](https://en.wikipedia.org/wiki/AVIF) – .avif
* [HEVC](https://en.wikipedia.org/wiki/High_Efficiency_Video_Coding)
* [JPEG XL](https://en.wikipedia.org/wiki/JPEG_XL) – .jxl
* [PDF](https://en.wikipedia.org/wiki/PDF) – .pdf

Extending Leptonica to support additional image formats is not desired because each format costs much resources for implementation and maintenance. But maybe it is possible to use an external library for image handling. Then only support for that library must be implemented.

Possible libraries:

* ffmpeg2 – https://ffmpeg.org/, LGPL v2.1+, jxl
* graphicsmagick – http://www.graphicsmagick.org/, MIT license, jxl
* libimlib2 – https://docs.enlightenment.org/api/imlib2/html/index.html, license?, heic / jxl
* others?
