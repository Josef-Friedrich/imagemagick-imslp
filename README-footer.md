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
