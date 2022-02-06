# PageXML

Cf. <https://ocr-d.de/en/gt-guidelines/trans/trPage.html>


You can check the validity of the PageXML using `xsltproc` and the PageXML schema file (cf. [this gh issue](https://github.com/OCR4all/LAREX/issues/302)).

```bash
wget "https://www.primaresearch.org/schema/PAGE/gts/pagecontent/2019-07-15/pagecontent.xsd"
xmllint --schema pagecontent.xsd --noout BOOK/processing/*.xml
```