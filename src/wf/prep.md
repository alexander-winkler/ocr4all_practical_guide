# Prepare your project

In order to start a new OCR4all project (usually a book), go to the `ocr4all` directory created during the [installation](./inst/installation_linux.md) of OCR4all.

```
.
└── ocr4all
    ├── data
    └── models
```

Go to the data directory and create a project folder and an `input` folder where you will put your scans.

```bash
# cd into the data directory
cd data

mkdir new_project

mkdir new_project/input
```

Copy the image files into `input` directory, either through the graphical interface (copy+paste) or in your Terminal:

```bash
cp path/to/download/img-*.png /path/to/ocr4all/data/new_project/input
```