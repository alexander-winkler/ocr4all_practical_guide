# Getting the images

Try to get scans in a decent quality.

Scans downloaded from Google Books being binarized and low-resolution are not the best choice.
If possible, try to get hold of high-quality scans provided by libraries.

A good starting point for your research are the following sites:

- [Deutsche Digitale Bibliothek (DDB)](https://www.deutsche-digitale-bibliothek.de/?lang=en): Aggregates digitizations from German GLAM institutions
- [Austrian National Library](https://www.onb.ac.at/en/): Offers many scans in good quality not retrievable via DDB

Ideally, you download the images as a bunch of single image files (png,jpg,tif).
Sometimes, however there is only a single pdf file available for download.

You can extract image files from the pdf using the `pdfimages` tool, which is part of `poppler-utils` and available [for linux](https://poppler.freedesktop.org/) and [MacOS](https://formulae.brew.sh/formula/poppler).

```bash
pdfimages -png YOUR_PDF_FILE.pdf img
```

This command will extract the images, convert them into the png-format and store them as `img-000.png img-001.png ...`.

If you must use a google books pdf you will get lots of 'noise' (the Google watermarks) which you will have to take care of in the [next step](./prep.md).


