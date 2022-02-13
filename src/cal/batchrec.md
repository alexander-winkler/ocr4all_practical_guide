# Batch Recognition

The basic command for text recognition with `calamari-predict` is the following:

```bash
 calamari-predict \
--data PageXML \
--data.text_index 1 \
--data.pred_extension ".xml" \
--data.images my_ocr4all_project/processing/*.bin.png \
--data.xml_files my_ocr4all_project/processing/*.xml \
--checkpoint models/0/1.ckpt.json
```

With this command you can run the Recognition process on more than one project.