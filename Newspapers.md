## Tesseract for historic newspapers

### UB Gießen

Create new OCR for Neue Tageszeitung, February 1914.

```
# Example how to get a single METS file.
curl -o 30170.xml "https://digisam.ub.uni-giessen.de/ubg-ihd-zuz/oai/?verb=GetRecord&metadataPrefix=mets&mode=view&identifier=30170"

# Get all METS files for February 1914.
idlist="30377 30384 30391 30398 30407 30414 30425 30434 30441 30450 30459 30466 30479 30488 30495 30502 30509 30516 30527 30534 30541 30548 30555 30562"
for id in $idlist; do curl -o $id.xml "https://digisam.ub.uni-giessen.de/ubg-ihd-zuz/oai/?verb=GetRecord&metadataPrefix=mets&identifier=$id"; done

# Get all related images in maximum resolution.
for url in $(cat $(grep -l webcache.0 *.xml)|sed 's/"/\n/g'|grep webcache.0); do id=$(basename $url); echo $id && curl -o $id.jpg "$url"; done

# Perform Tesseract OCR with model ubma/frak2021_1.069. Run single-threaded.
export LANG=C.UTF-8
mkdir ocr
time -p (for img in *.jpg; do echo $img && time -p tesseract $img ocr/$(basename $img .jpg) -l ubma/frak2021_1.069 alto hocr txt; done) 2>&1 | tee ocr.log

# Perform Tesseract OCR with model ubma/german_newspapers and get images on the fly via their URL. Use all CPU cores.
time -p for url in $(cat $(grep -l webcache.0 *.xml)|sed 's/"/\n/g'|grep webcache.0); do id=$(basename $url); echo $id; done | parallel nice tesseract https://digisam.ub.uni-giessen.de/download/webcache/0/{} ../german_newspapers/ocr/{} -l ubma/frak2021_1.069 alto hocr txt 2>&1 | tee ../german_newspapers/ocr/ocr.log
```