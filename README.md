[![Build Status](https://travis-ci.org/Josef-Friedrich/imagemagick-imslp.sh.svg?branch=master)](https://travis-ci.org/Josef-Friedrich/imagemagick-imslp.sh)

# imagemagick-imslp.sh


## Summary / Short description

> A wrapper script for imagemagick to process image files suitable for imslp.org (International Music Score Library Project)

## Usage

```
Usage: imagemagick-imslp.sh [-bcfhijrSstv] <filename-or-glob-pattern>

A wrapper script for imagemagick to process image files suitable for imslp.org (International Music Score Library Project)

http://imslp.org/wiki/IMSLP:Musiknoten_beisteuern

OPTIONS:
	-b, --backup
	  Backup original images (add .bak to filename).
	-c, --compression
	  Use CCITT Group 4 compression. This options generates a PDF
	  file.
	-e, --enlighten-border
	  Enlighten the border.
	-f, --force
	  force
	-h, --help
	  Show this help message
	-i, --imslp
	  Use the best options to publish on IMSLP. (--compress,
	   --join, --resize)
	-j, --join
	  Join single paged PDF files to one PDF file
	-r, --resize
	  Resize 200%
	-S, --threshold-series
	  Convert the samge image with different threshold values to
	  find the best threshold value. Those values are probed:
	  50 55 60 65 70 75.
	-s, --short-description
	  Show a short description / summary.
	-t, --threshold
	  threshold, default 50%.
	-v, --version
	  Show the version number of this script.

DEPENDENCIES:

	- pdftk
	- imagemagick (convert, identify)
	- poppler (pdfimages)

```

## Project pages

* https://github.com/Josef-Friedrich/imagemagick-imslp.sh

## Testing

```
make test
```

## TODO

* Fix and test --enlighten-border

## Example

Original file size: 1.1 MB

![](test/scans/readme/original.png)

```sh
magick convert original.png -deskew 40% deskew.png
```

![](test/scans/readme/deskew.png)

```sh
magick convert deskew.png -trim +repage repage.png
```

![](test/scans/readme/repage.png)

```sh
magick convert repage.png \
  -region 1449x29 -level 0%,30% \
  -region 29x992+1449 -level 0%,30% \
  -region 1449x29+29+992 -level 0%,30% \
  -region 29x992+0+29 -level 0%,30% \
  border-lighten.png
```

![](test/scans/readme/border-lighten.png)

```sh
magick convert border-lighten.png -resize 200% resize.png
```

![](test/scans/readme/resize.png)

```sh
magick convert resize.png -threshold 70% threshold.png
```

![](test/scans/readme/threshold.png)

```sh
magick convert threshold.png -trim +repage repage2.png
```

![](test/scans/readme/repage2.png)

```sh
magick convert repage2.png -compress Group4 -monochrome compress.pdf
```

![](test/scans/readme/repage2.png)

Final file size: 52 KB
