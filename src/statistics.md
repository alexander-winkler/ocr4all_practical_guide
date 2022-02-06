# Some statistics

OCR4all doesn't provide any statistics on your projects.

Some simple command line operations can be helpful.

## Page numbers

How many pages are there in my project?

```bash
ls project/input/*.png | wc -l
```

## Number of lines

This command prints you a list of line numbers:

```bash
xmllint --xpath "count(//*[local-name()='TextEquiv'])" project/processing/*.xml
```

You can sum up the numbers in the list like this:

```bash
xmllint --xpath "count(//*[local-name()='TextEquiv'])" project/processing/*.xml | awk '{sum+=$1} END{print sum}'
```

#### Number of lines of Grount Truth

To find out how many lines of Ground Truth you have in one or multiple project(s), use

```bash
xmllint --xpath "count(//*[local-name()='TextEquiv'][@index='0']/*[local-name()='Unicode'])" project/processing/*.xml | awk '{sum+=$1} END{print sum}'
```

If you want to ouput the percentage of lines that have GT, the command start getting a bit unwieldy:

```bash
echo $(xmllint --xpath "count(//*[local-name()='TextEquiv'][@index='0']/*[local-name()='Unicode'])" project/processing/*.xml | awk '{sum+=$1} END{print sum}')/$(xmllint --xpath "count(//*[local-name()='TextEquiv'])" project/processing/*.xml | awk '{sum+=$1} END{print sum}') | bc -l
```