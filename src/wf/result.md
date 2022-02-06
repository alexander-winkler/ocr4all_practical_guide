# Result Generation









## Quick'n'dirty

To extract text on the fly, you can resort to the command line:

```bash
# Only Ground Truth
xmllint --xpath "//*[local-name()='TextEquiv'][@index='0']/*[local-name()='Unicode']/text()" project/processing/*.xml

# Only OCR
xmllint --xpath "//*[local-name()='TextEquiv'][@index='1']/*[local-name()='Unicode']/text()" project/processing/*.xml

# Ground Truth where available, otherwise OCR
xmllint --xpath "//*[local-name()='TextEquiv'][@index='0']/*[local-name()='Unicode']/text() | //*[local-name()='TextEquiv'][@index='1' and not(../*[local-name()='TextEquiv'][@index='0'])]/*[local-name()='Unicode']/text()" project/processing/*.xml
```