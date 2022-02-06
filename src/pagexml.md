# PageXML

## Purpose and structure

The PageXML is the one file that stores all information generated during the OCR pipeline.

It contains 
- metadata on the image file (filename and dimensions)
- information on text regions
- text lines
- OCR text
- Ground Truth (where available)

It is an XML file that can become very verbose but has the following basic structure:

```xml
<?xml version="1.0"?>
<PcGts xmlns="http://schema.primaresearch.org/PAGE/gts/pagecontent/2019-07-15" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schema.primaresearch.org/PAGE/gts/pagecontent/2019-07-15 http://schema.primaresearch.org/PAGE/gts/pagecontent/2019-07-15/pagecontent.xsd">
  <Metadata>
    <Creator>CREATOR</Creator>
    <Created>DATE</Created>
    <LastChange>TIMESTAMP</LastChange>
  </Metadata>
  <Page imageFilename="FILENAME" imageHeight="HEIGHT" imageWidth="WIDTH">
    <TextRegion id="REGION_ID" type="paragraph" orientation="ORIENTATION">
      <Coords points="POLYGON"/>
      <TextLine id="LINE_ID">
        <Coords points="POLYGON"/>
        <Word id="WORD_ID">
          <Coords points="POLYGON"/>
          <Glyph id="GLYPH_ID">
            <Coords points="POLYGON"/>
            <TextEquiv index="1" conf="RECOGNITION CONFIDENCE">
              <Unicode>OCR GLYPH</Unicode>
            </TextEquiv>
          more glyphs ...
        <TextEquiv index="1" conf="RECOGNITION CONFIDENCE">
            <Unicode>OCR WORD</Unicode>
          </TextEquiv>
        </Word>
        more words
        <TextEquiv index="1" conf="RECOGNITION CONFIDENCE">
          <Unicode>OCR LINE</Unicode>
        </TextEquiv>
        <TextEquiv index="0">
          <Unicode>GROUND TRUTH (if available)</Unicode>
        </TextEquiv>
      </TextLine>
      more lines ...
    </TextRegion>
  </Page>
</PcGts>
```

This essentially breaks down to metadata (`<Metatdata/>`) and OCR information on line (`<TextLine/>`), word (`<Word/>`) and glyph level (`<Glyph/>`).
For glyphs and lines, a confidence value is provided.
It tells you how certain the OCR engine is about the result. 

Regions, lines, words, and glyphs also have a `<Coords/>` node which contains the polygon vertices of the corresponding image area.

The Ground Truth you input (cf. [Ground Truth Production](./gt.md))is stored on line level in an `<TextEquiv>` element with `@index="0"`.


## Technical Information
Cf. <https://ocr-d.de/en/gt-guidelines/trans/trPage.html>


## Validation

You can check the validity of the PageXML using `xsltproc` and the PageXML schema file (cf. [this gh issue](https://github.com/OCR4all/LAREX/issues/302)).

```bash
wget "https://www.primaresearch.org/schema/PAGE/gts/pagecontent/2019-07-15/pagecontent.xsd"
xmllint --schema pagecontent.xsd --noout BOOK/processing/*.xml
```

If you have some PageXML files that were produced with an older version of OCR4all, you might encounter the problem that your PageXML is overwritten.

The reason for this is that in previous versions of OCR4all PageXMLs coordinates could be negative as well.

This is not compatible with the PageXML specifications and triggers this behaviour.
To avoid data loss, update your OCR4all to this, you have to do a particular XSLT (cf. [this GH issue](https://github.com/OCR4all/LAREX/issues/302)):

```bash
wget "https://raw.githubusercontent.com/bertsky/workflow-configuration/master/page-fix-coords.xsl"

mkdir tmp_output

for i in BOOK/processing/*.xml; \
    do xsltproc -o tmp_output/$(basename $i) page-fix-coords.xsl $i; \
    done
```