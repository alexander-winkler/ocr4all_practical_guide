# Calamari Installation

The installation of calamari can be a pain.
At the time of writing (13.2.22), installation via pip doesn't seem to work properly.

It is better to install it from source.

For a clean and fresh calamari installation, let's clone the git repository:

```bash
git clone https://github.com/calamari-OCR/calamari
```

Then create a virtual environment (to keep things simple, I put the virtual environment folder into the calamari folder):

```bash

cd calamari

mkdir venv

python3.7 -m venv venv

source venv/bin/activate
```

The virual environment is active, so now you can run the `setup.py`:

```bash
python setup.py install
```

When you run `calamari-predict` for the first time, you will see a number of error messages according to which you are lacking required packages. 

You will have to run a number of `pip install <package name>` to install what is required.

I have created a [`requirements.txt`](./cal/requirements.txt) for the virtual environment of my current Calamari (`v2.2.0`) installation (`pip freeze --local > requirements.txt`).

So you could download the `requirements.txt` and try to run

```bash

pip install -r requirements.txt
```


