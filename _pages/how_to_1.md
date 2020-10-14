---
layout: default
title: How to XYZ? - Part 1
---

# How to XYZ? - Part 1
##### 13-Oct-2020

### How to merge multiple PDF files?
[ghostscript](https://en.wikipedia.org/wiki/Ghostscript) is a software for processing Adobe's [PostScript](https://en.wikipedia.org/wiki/PostScript) and [PDF](https://en.wikipedia.org/wiki/Portable_Document_Format) [page description languages](https://en.wikipedia.org/wiki/Page_description_language). It may be used to merge multiple PDF files into a single PDF file, using the following command line syntax:
```Shell
gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=combined.pdf -dBATCH pdf1.pdf pdf2.pdf pdf3.pdf ...
```

