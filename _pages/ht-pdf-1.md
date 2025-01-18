---
layout: default
title: Dealing with PDF files
---

# Dealing with PDF files

The starting point of this investigation was how to mitigate security risks associated with PDF files from unknown sources. A PDF file may have embedded JavaScript which can be malicious. So the goals are:
1. How to find if a PDF file contains embedded JavaScript or not?
2. If a PDF file contains JavaScript, how to remove it from the file?
3. Can we disable execution of JavaScript in PDF reader software?
<br/>

### Checking PDF file for embedded JavaScript
1. [iText](https://en.wikipedia.org/wiki/IText) is a library for creating and manipulating PDF files in Java and .NET. RUPS is a product built on top of iText. It has two code repositories: [rups](https://github.com/itext/rups) (deprecated) and [i7j-rups](https://github.com/itext/i7j-rups). RUPS allow to visually inspect the structure of a PDF file. iText library allows to extract embedded objects/streams. Follwoing links may be helpful.
    * [RUPS: Looking inside your PDFs](https://itextpdf.com/blog/technical-notes/rups-looking-inside-your-pdfs)
    * [How to extract embedded streams?](https://kb.itextpdf.com/itext/how-to-extract-embedded-streams)
    * [Extracting objects from a PDF](https://kb.itextpdf.com/itext/extracting-objects-from-a-pdf)

2. Another suite of tools is the [Poppler](https://en.wikipedia.org/wiki/Poppler_(software)) library, and the associated collection of command line utilities called [poppler-utils](https://packages.debian.org/search?keywords=poppler-utils). Of these, `pdfinfo` can report if a PDF file contains JavaScript, and it can also print it out. Particularly,
    * Output of the command `pdfinfo <file>` contains a line beginning with `JavaScript`. For example, `JavaScript:      no` or `JavaScript:      yes`
    * `pdfinfo -js <file>` prints all JavaScript code in the PDF, allowing to inspect it.
    * Other commands in poppler-utils package are: `pdfattach`, `pdfdetach`, `pdffonts`, `pdfimages`, `pdfinfo`, `pdfseparate`, `pdfsig`, `pdftocairo`, `pdftohtml`, `pdftoppm`, `pdftops`, `pdftotext`, `pdfunite`. Here is a brief description of these.
        * `pdfattach` – add a new embedded file (attachment) to an existing PDF
        * `pdfdetach` – extract embedded documents from a PDF
        * `pdffonts` – lists the fonts used in a PDF
        * `pdfimages` – extract all embedded images at native resolution from a PDF
        * `pdfinfo` – list all information of a PDF
        * `pdfseparate` – extract single pages from a PDF
        * `pdfsig` - PDF digital signatures tool
        * `pdftocairo` – convert single pages from a PDF to vector or bitmap formats using cairo
        * `pdftohtml` – convert PDF to HTML format retaining formatting
        * `pdftoppm` – convert a PDF page to a bitmap
        * `pdftops` – convert PDF to printable PS format
        * `pdftotext` – extract all text from PDF
        * `pdfunite` – merges several PDFs

3. The embedded JavaScript may some times be viewed by opening a PDF file in a text editor. However, this is not a guaranteed way, because the JavaScript code may be compressed and embedded in a stream. In this case, it will not be readable in a text editor.
<br/>

### Removing embedded JavaScript from a PDF file
1. Reportedly, printing a PDF file using "Print to PDF" printer driver will create a PDF file without JavaScript. However, I have not tried this, for want of a PDF file that contains JavaScript.
2. Reportedly, the above mentioned RUPS software may be used to remove embedded JavaScript from PDF files. Again, I have not tried this.
3. Adobe Acrobat &mdash; not Adobe Acrobat Reader &mdash; software allows to edit the file, and remove embedded JavaScript from it.
<br/>

### Disabling execution of JavaScript in PDF reader software
* Generally, PDF readers that support JavaScript execution provide a setting to disable the execution. [Here](https://helpx.adobe.com/acrobat/using/javascripts-pdfs-security-risk.html) are instructions for Adobe Acrobat Reader.
* It would be even better, if the PDF reader cannot execute JavaScript at all. Based on a discussion forum post, **apparently** [Xreader](https://github.com/linuxmint/xreader) document viewer &mdash; the default PDF reader in Linux Mint OS &mdash; cannot execute JavaScript. However, I could not verify this from the official documentation. The command line options of Xreader can be looked up in man pages, and are also available [here](https://man.archlinux.org/man/xreader.1.en). This documentation is mute about JavaScript execution.
 <br/>


