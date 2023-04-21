# Häufige Fragen und Antworten

Die Sammlung hier kann gerne ergänzt werden. Auch Übersetzungen der englischsprachigen FAQ sind willkommen.

## Wie starte ich eine OCR? Hat jemand für mich einen Beispielkommandozeilenaufruf?
```
tesseract https://digi.bib.uni-mannheim.de/fileadmin/vl/ubmaosi/59088/max/59088_0008.jpg -
```
Dieses Beispiel nutzt das Feature, dass aktuelle Tesseract-Versionen auch OCR auf ein per URL angegebenes Bild machen können.
Das OCR-Ergebnis gibt Tesseract in der Konsole direkt aus.
Und ein Modell ist nicht angegeben. Daher wird das immer installierte eng.traineddata verwendet.
Der Installer installiert einen Konsolenaufruf, bei dem der Suchpfad für tesseract bereit richtig eingestellt ist. Wenn man den nicht verwendet, muss man vor tesseract den kompletten Installationspfad ergänzen. Ansonsten sind die Aufrufe unter Windows und Linux identisch.

Das minimalistische Beispiel oben lässt sich einfach erweitern, z. B. mit Ausgabe in Datei(en) unterschiedlicher Formate und einem Modell, das für deutschsprachige Texte optimiert ist:
```
tesseract https://digi.bib.uni-mannheim.de/fileadmin/vl/ubmaosi/59088/max/59088_0008.jpg ergebnis -l deu alto hocr tsv txt pdf
```
Dieser Aufruf erzeugt ergebnis.xml (ALTO XML), ergebnis.hocr (hOCR / HTML), ergebnis.tsv (TSV), ergebnis.txt (Textdatei) und ergebnis.pdf (PDF).

Jeder Aufruf von `tesseract` kann genau eine Bilddatei (also typischerweise eine Seite) verarbeiten.
Statt der URL einer Bilddatei können natürlich auch lokal abgelegte Dateien (gegebenenfalls mit ihrem Pfad) angegeben werden.
Datei werden viele gängige Bildformate unterstützt, insbesondere jpg, jp2, png, tif, bmp und weitere.

## Wie installiere ich zusätzliche Modelle unter Windows?

Mit `tesseract --list-langs` gekommt man angezeigt, welche Modelle bereits installiert sind.
Zusätzliche zeigt dieser Befehl in der ersten Zeile der Ausgabe an, in welchem Verzeichnis die Modelle liegen.
Zusätzliche Modelle lassen sich dort (wahlweise in Unterverzeichnissen) hinzufügen.

## Which models can be used for historic European texts?

Old European texts often use [Fraktur](https://en.wikipedia.org/wiki/Fraktur) or historic [Antiqua](https://en.wikipedia.org/wiki/Antiqua_(typeface_class)) fonts with [long s](https://en.wikipedia.org/wiki/Long_s) and [ligatures](https://en.wikipedia.org/wiki/Orthographic_ligature). Those texts require special Tesseract models as the standard models like `eng`, `deu` or `script/Latin` don't recognize them good.

Several models are available for such old texts. `deu_frak` is a model which was trained for Tesseract 3. The current standard models are `frk` and `script/Fraktur`. In addition, there exist models trained by UB Mannheim which often give better results.

### deu_frak

This user contributed model only supports the legacy (pattern based) OCR engine, so does not work with a LSTM neural network which typically can achieve better OCR results. The legacy engine has one advantage: it can detect character attributes like cursive or fat.

### frk

This is the standard model for German Fraktur texts. It includes a German dictionary. The model has some restrictions regarding the character set which it can recognize. It also has problems especially with `ch` and `ck` ligatures.

### script/Fraktur

This is the standard model for European Fraktur and historic Antiqua texts. It supports a wider character set than `frk`, but has similar problems with `ch` and `ck`.

### Fraktur models from UB Mannheim

Those models typically give the best results. They eliminate the problems of `frk` and `script/Fraktur` and know different variants of the German umlauts. These variants are available:

- [models](https://ub-backup.bib.uni-mannheim.de/~stweil/ocrd-train/data/Fraktur_5000000/tessdata_fast/) based on `script/Fraktur`
- [models](https://ub-backup.bib.uni-mannheim.de/~stweil/ocrd-train/data/GT4HistOCR_5000000/tessdata_fast/) trained from scratch
- [models](https://ub-backup.bib.uni-mannheim.de/~stweil/ocrd-train/data/ONB/tessdata_fast/) trained from Austrian newspapers with Fraktur
- [latest models](https://ub-backup.bib.uni-mannheim.de/~stweil/tesstrain/frak2021/tessdata_fast/) trained in 2021 (not always the best)

All those models work without any dictionary. Older Tesseract versions therefore show a warning which can simply be ignored.
[frak2021_1.069](https://ub-backup.bib.uni-mannheim.de/~stweil/tesstrain/frak2021/tessdata_fast/frak2021_1.069.traineddata) is a model where we added a dictionary.
