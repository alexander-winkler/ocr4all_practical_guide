# Training of Mixed Models

[maxnth](https://github.com/maxnth) has kindly provided the command for the training of mixed models based on OCR4all GT in [this Github Issue](https://github.com/OCR4all/OCR4all/issues/66):

```bash
calamari-cross-fold-train \
--files /path/to/first/ocr4all/project/processing/*.bin.png /path/to/second/ocr4all/project/processing/*.bin.png \
--dataset PAGEXML \
--n_folds 5 \
--num_threads 56 \
--best_models_dir /some/dir/models \
--display 100 \
--batch_size 5 \
--temporary_dir /some/dir/tmp \
--text_regularization spaces \
--n_augmentation 5
```