# Lightning Talks

Really messy!


# 1. Linting

Originally a C program by Stephen Johnson, 1978 paper.

AST, checks against rules.

Checks code more strictly than a compiler for syntax, consistency, style

Linters are lint-like programs for many languages.


## Purpose

Less Debugging, Looking for logic loopholes, Carving out dead code, Reduce runtime errors, For big teams: Consistency, Interpreted languages - no compile time


## Uses

Unused variables, functions, dead code, undeclared/unset vars, enforcefunction argument/parameter checking... etc.


## Style Checking

Code looks fine but is inconsistent.  You know the stuff, PEP8.  Consistency.


## Python

Flake8, PyLint, PyFlakes, Pep8


## For editors

vim - flake8

emacs - ?


## Custom lint rules

You can write a plugin that examines whatever can be checked by AST, etc.


## Also you can write little rulesets that "lint" your code by rules


# 2. Zebras and Lasers - Jonas Neubert - Zymergen

Talk about barcode readers.

Writes software stuck in a box for factories.

The laser takes samples over time, so you have to do image processing.

You thing opencv = image processing. I think LIST COMPREHENSIONS.

`kernel = lambda a,b,c: a if a==c!=b else b`

`smooth = ''.join([(a,b,c) for a,b,c in zip(data[0:], data[1:], data[2:])])`

`[str(round(len(list(v))/4.0)) for k,v in itertools.groupby(smooth)][1:-1]`

Look up what you got on the wikipedia table of barcodes


# 3. 2FA, OTP, WTF - Making technical concepts accessible - Kelly

Who here works on a website where people sign up or login? Congrats you are a security engineer.

Get your family using `password managers` and `2FA`.

## Factors: Something you know, something you have, something you are

Use this stuff.


# 4. Gert, Scientist @ Nasa working on Kepler satellite

Kepler looks at the brightness of stars and if you look long enough the brightness dims for 6 hours once a year.

You can find a planet using 7-8 lines of python.

I am going to find a planet around a distant star live on stage.

`python3, numpy, scipy.signal, matplotlib working in a jupyter notebook`

Use a low pass filter to remove long term trend in star brightness data, this normalizes the year.

Next, a `lomb-scargle periodogram` or something is used to find periodic signal in the data.

The planet has a 0.84 day orbit, so the data was aggregated daily.

Python package: `PyKE` - come talk to us if you want to be a developer or intern at nasa.


# 5. Bot Cars! - John Ellis

Race course out in oakland once a month, the cars look like RC type cars.

Were are these events? Huge warehouse in oakland!!

## Behavior cloning is what we do. 

- Other techniques: You can do line following, something else...
- Data labeling is tough in machine learning. Having a data labeler system expidites that.

## Toolchain
- Camera input device
- OpenCV, B4L2 capture, python3
- Adafruit BNO005 gyroscope, dualshock4+ds4drv controller, usb2 camera v4l2capture
- nvidia jetson tx2 + orbitty carrier
- pololu micromaester + libusb
- Cycloid: Traxxas Chassis
- Donkeycar: raspberry pi, 3dprinted superstruture, ~$200
- Derp Learning: Nvidia TX1, Traxxas Slash, ~$800
    - put a gpu on your car so you have no delay and can learn on board
- Virtual test environment - use a graphics engine in unity
    - you can use numpy+scikit image but it has its limits, he did it
  

# 6. Quilt - Docker, but for Data - Anish 

`akarve/pydatabook` - an example

## Why?

- Code has reusable building blocks, github, PyPI, DockerHub
- Data is missing reusable building blocks - stuff like s3, github, everywhere online
- Data packages: metadata and serialized


## Package Lifecycle - 3-4 primitives that matter
    - build, , install, import
    - `quilt build` - shred them into a dataframe, hash, stick into a hash tree, serialize columnar data, indexing

## Why track in a hash tree? - Need to be able to send all the deltas

If you just change a readme, just want to download that on a version update


## Catalog is like PyPI but for data

[his book on quiltdata.com](http://quiltdata.com/package/akarve/pydata_book)

`from quilt.data.akarve import pydata_book as pb` - `pb.getdata.train() (or something)` and you get a dataframe out.

Working on react+Tensorflow, R, Spark, going to get stuff into Jupyter.


# Datasette - Simon @ Eventbrite - journalist stuff @ guardian

[datasette](github.com/simonw/datasette/)

Make an instant, read-only JSON API for any SQLite database. It also provides tools for packaging the database as a docker container and deploying to hosting providers.

Arbitrary SQL is pretty fine, you can't really modify the data, read only. Chrome history example.

San Francisco open data portal, data.sfgov.org - download csv of trees from the city

Wrote [csvs2sqlite] which just turns the CSV to a sqlite3 database. Can refactor csv to something a bit more relational. Extract some columns... He list about 12 columns he wants into separate tables. Also he uses `-x` to make the columns searchable in sqlite, indexing or whatever?

`$ datasette tree.db`

`$ datasette publish now sf-trees.db` - gives you a URL, hyperlinks.

Just like that you have a browseable, searchable json API

he built `https://sf-tree-search.now.sh` because he thought "why not?" - search sf by tree

