#Tesseract at UB Mannheim

The Mannheim University Library (UB Mannheim) uses Tesseract to perform OCR
of historical German newspapers ([Allgemeine Preußische Staatszeitung](https://de.wikipedia.org/wiki/Allgemeine_Preu%C3%9Fische_Staatszeitung), [Deutscher Reichsanzeiger](https://de.wikipedia.org/wiki/Deutscher_Reichsanzeiger)).

Normally we run Tesseract on Debian GNU Linux, but there was also the need for
a Windows version. That's why we have built a Tesseract installer for Windows.

The latest installer can be downloaded here:
[tesseract-ocr-setup-3.05.00dev.exe](http://digi.bib.uni-mannheim.de/tesseract/tesseract-ocr-setup-3.05.00dev.exe). There may be also [older versions](http://digi.bib.uni-mannheim.de/tesseract/) available.

History:
* 2016-07-11 TIFF warnings are now shown on the console (no longer disturbing message windows).
* 2016-05-13 The new installer now includes the executables needed for training, too. It is based on the latest Tesseract sources.
